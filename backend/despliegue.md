# Despliegue backend

Esta guía explica cómo desplegar el backend de GoalApp en diferentes entornos, desde desarrollo local hasta producción.

***

### 1. Requisitos Previos

#### Software Necesario

| Requisito | Versión | Descripción |
|-----------|---------|-------------|
| Python | 3.10+ | Intérprete de Python |
| MySQL | 8.0+ | Base de datos relacional |
| pip | 21+ | Gestor de paquetes Python |
| Git | 2.x | Control de versiones |

#### Opcional (para producción)

| Requisito | Descripción |
|-----------|-------------|
| Docker | Contenedores para despliegue |
| Nginx | Proxy inverso |
| Gunicorn | Servidor WSGI de producción |

***

### 2. Configuración del Entorno

#### Clonar el repositorio

```bash
git clone https://github.com/tu-usuario/goalapp.git
cd goalapp/backend
```

#### Crear entorno virtual

**Windows (PowerShell):**

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

**Linux/Mac:**

```bash
python -m venv .venv
source .venv/bin/activate
```

#### Instalar dependencias

```bash
pip install -r requirements.txt
```

**Contenido de requirements.txt:**

```
fastapi
uvicorn[standard]
sqlalchemy
pymysql
alembic
python-dotenv
pydantic[email]
pydantic-settings
python-jose
passlib[bcrypt]
python-multipart
cryptography
```

***

### 3. Variables de Entorno

#### Crear archivo .env

```bash
cp .env.example .env
```

#### Configuración completa (.env)

```env
# ============================================================
# CONFIGURACIÓN DE LA BASE DE DATOS
# ============================================================
DATABASE_URL=mysql+pymysql://usuario:password@localhost:3306/futbol_app
DATABASE_ECHO=True

# ============================================================
# CONFIGURACIÓN DE SEGURIDAD JWT
# ============================================================
# Generar clave segura con: python -c "import secrets; print(secrets.token_urlsafe(64))"
SECRET_KEY=tu_clave_secreta_aqui_cambiar
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=60

# ============================================================
# CONFIGURACIÓN DE LA APLICACIÓN
# ============================================================
APP_NAME=Liga Amateur App
API_VERSION=v1
ENVIRONMENT=development
PORT=8000
HOST=0.0.0.0

# ============================================================
# CONFIGURACIÓN DE CORS
# ============================================================
CORS_ORIGINS=http://localhost:3000,http://localhost:5173,http://localhost:8081

# ============================================================
# CONFIGURACIÓN DE LOGGING
# ============================================================
LOG_LEVEL=INFO
```

#### Descripción de Variables

| Variable | Descripción | Ejemplo |
|----------|-------------|---------|
| `DATABASE_URL` | URL de conexión a MySQL | `mysql+pymysql://user:pass@host:3306/db` |
| `DATABASE_ECHO` | Mostrar SQL en consola | `True` (desarrollo), `False` (producción) |
| `SECRET_KEY` | Clave para firmar JWT | Generar con `secrets.token_urlsafe(64)` |
| `ALGORITHM` | Algoritmo de firma JWT | `HS256` |
| `ACCESS_TOKEN_EXPIRE_MINUTES` | Tiempo de vida del token | `60` |
| `APP_NAME` | Nombre de la aplicación | `Liga Amateur App` |
| `API_VERSION` | Versión de la API | `v1` |
| `ENVIRONMENT` | Entorno de ejecución | `development` o `production` |
| `PORT` | Puerto del servidor | `8000` |
| `HOST` | Host del servidor | `0.0.0.0` (todas las interfaces) |
| `CORS_ORIGINS` | Orígenes permitidos (separados por coma) | `http://localhost:3000` |
| `LOG_LEVEL` | Nivel de logging | `DEBUG`, `INFO`, `WARNING`, `ERROR` |

***

### 4. Configuración de Base de Datos

#### Crear base de datos MySQL

```sql
CREATE DATABASE futbol_app CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE USER 'goalapp_user'@'localhost' IDENTIFIED BY 'contrasena_segura';
GRANT ALL PRIVILEGES ON futbol_app.* TO 'goalapp_user'@'localhost';
FLUSH PRIVILEGES;
```

#### Inicializar tablas

El backend crea automáticamente las tablas al iniciar mediante SQLAlchemy:

```python
# En app/main.py
Base.metadata.create_all(bind=engine)
```

**Alternativa con script SQL:**

```bash
mysql -u goalapp_user -p futbol_app < app/database/init.sql
```

***

### 5. Ejecución en Desarrollo

#### Iniciar el servidor

**Opción 1: Con uvicorn directamente**

```bash
uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

**Opción 2: Ejecutando el módulo**

```bash
python -m app.main
```

**Opción 3: Desde el archivo main.py**

```bash
python app/main.py
```

#### Verificar que funciona

```bash
# Health check
curl http://localhost:8000/health

# Respuesta esperada
{
    "status": "healthy",
    "app": "Liga Amateur App",
    "version": "v1",
    "environment": "development"
}
```

#### Documentación interactiva

- Swagger UI: http://localhost:8000/docs
- ReDoc: http://localhost:8000/redoc

***

### 6. Ejecución en Producción

#### Configurar variables de producción

```env
ENVIRONMENT=production
DATABASE_ECHO=False
LOG_LEVEL=WARNING
HOST=0.0.0.0
PORT=8000
```

#### Usar Gunicorn con Uvicorn workers

```bash
gunicorn app.main:app \
    --workers 4 \
    --worker-class uvicorn.workers.UvicornWorker \
    --bind 0.0.0.0:8000 \
    --timeout 120 \
    --keep-alive 5
```

#### Parámetros recomendados

| Parámetro | Valor | Descripción |
|-----------|-------|-------------|
| `--workers` | 4 | Número de workers (CPU cores * 2 + 1) |
| `--worker-class` | uvicorn.workers.UvicornWorker | Worker async para FastAPI |
| `--timeout` | 120 | Timeout en segundos |
| `--keep-alive` | 5 | Keep-alive en segundos |

***

### 7. Despliegue con Docker

#### Dockerfile

```dockerfile
FROM python:3.11-slim

WORKDIR /app

# Instalar dependencias del sistema
RUN apt-get update && apt-get install -y \
    gcc \
    default-libmysqlclient-dev \
    pkg-config \
    && rm -rf /var/lib/apt/lists/*

# Copiar requirements y instalar dependencias
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copiar código de la aplicación
COPY . .

# Exponer puerto
EXPOSE 8000

# Comando por defecto
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
```

#### Construir imagen

```bash
docker build -t goalapp-backend:latest .
```

#### Ejecutar contenedor

```bash
docker run -d \
    --name goalapp-api \
    -p 8000:8000 \
    --env-file .env \
    goalapp-backend:latest
```

#### Docker Compose (con MySQL)

```yaml
version: '3.8'

services:
  db:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: root_password
      MYSQL_DATABASE: futbol_app
      MYSQL_USER: goalapp_user
      MYSQL_PASSWORD: goalapp_password
    volumes:
      - mysql_data:/var/lib/mysql
      - ./app/database/init.sql:/docker-entrypoint-initdb.d/init.sql
    ports:
      - "3306:3306"

  api:
    build: .
    ports:
      - "8000:8000"
    environment:
      DATABASE_URL: mysql+pymysql://goalapp_user:goalapp_password@db:3306/futbol_app
      DATABASE_ECHO: "False"
      SECRET_KEY: ${SECRET_KEY}
      ALGORITHM: HS256
      ACCESS_TOKEN_EXPIRE_MINUTES: 60
      APP_NAME: Liga Amateur App
      API_VERSION: v1
      ENVIRONMENT: production
      PORT: 8000
      HOST: 0.0.0.0
      CORS_ORIGINS: http://localhost:3000
      LOG_LEVEL: INFO
    depends_on:
      - db

volumes:
  mysql_data:
```

```bash
docker-compose up -d
```

***

### 8. Proxy Inverso con Nginx

#### Configuración de Nginx

```nginx
server {
    listen 80;
    server_name api.goalapp.com;

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        # Timeouts
        proxy_connect_timeout 60s;
        proxy_send_timeout 60s;
        proxy_read_timeout 60s;
    }
}
```

#### HTTPS con Certbot (Let's Encrypt)

```bash
# Instalar certbot
sudo apt install certbot python3-certbot-nginx

# Generar certificado
sudo certbot --nginx -d api.goalapp.com

# Renovar automáticamente
sudo certbot renew --dry-run
```

***

### 9. Verificación del Despliegue

#### Health Check

```bash
curl http://localhost:8000/health
```

**Respuesta esperada:**

```json
{
    "status": "healthy",
    "app": "Liga Amateur App",
    "version": "v1",
    "environment": "production"
}
```

#### Verificar conexión a base de datos

```bash
curl http://localhost:8000/api/v1/ligas/
```

**Respuesta esperada (si hay datos):**

```json
[
    {"id_liga": 1, "nombre": "Liga Municipal", ...}
]
```

#### Verificar autenticación

```bash
# Login
curl -X POST http://localhost:8000/api/v1/auth/login \
    -H "Content-Type: application/x-www-form-urlencoded" \
    -d "username=admin@email.com&password=password123"

# Usar token
curl http://localhost:8000/api/v1/auth/me \
    -H "Authorization: Bearer <token>"
```

***

### 10. Logs y Monitoreo

#### Niveles de Log

| Nivel | Uso |
|-------|-----|
| DEBUG | Información detallada para depuración |
| INFO | Confirmación de operaciones normales |
| WARNING | Algo inesperado pero no crítico |
| ERROR | Error serio, la aplicación continúa |
| CRITICAL | Error crítico, la aplicación no puede continuar |

#### Ver logs en tiempo real

```bash
# Con uvicorn
uvicorn app.main:app --log-level info

# Con gunicorn
gunicorn app.main:app --log-level info --access-logfile - --error-logfile -
```

#### Logs estructurados (recomendado para producción)

```bash
pip install python-json-logger
```

***

### 11. Solución de Problemas Comunes

#### Error de conexión a base de datos

```
sqlalchemy.exc.OperationalError: (pymysql.err.OperationalError) Can't connect to MySQL server
```

**Solución:**
- Verificar que MySQL esté ejecutándose
- Comprobar credenciales en DATABASE_URL
- Verificar que el usuario tenga permisos

#### Error de CORS

```
Access to XMLHttpRequest at 'http://localhost:8000' from origin 'http://localhost:3000' has been blocked by CORS policy
```

**Solución:**
- Añadir origen en CORS_ORIGINS
- Verificar middleware de CORS en main.py

#### Token JWT inválido

```
{"detail": "Token inválido o expirado"}
```

**Solución:**
- Verificar que SECRET_KEY sea la misma que se usó para crear el token
- Comprobar que el token no haya expirado
- Usar /auth/refresh para renovar token

#### Error de importación de módulos

```
ModuleNotFoundError: No module named 'app'
```

**Solución:**
- Ejecutar desde el directorio backend/
- Verificar que el entorno virtual esté activado
- Verificar PYTHONPATH

***

### 12. Checklist de Producción

- [ ] Cambiar `ENVIRONMENT` a `production`
- [ ] Cambiar `DATABASE_ECHO` a `False`
- [ ] Generar `SECRET_KEY` segura y única
- [ ] Configurar `CORS_ORIGINS` con dominios de producción
- [ ] Configurar base de datos con usuario dedicado
- [ ] Configurar HTTPS con certificado SSL
- [ ] Configurar backup de base de datos
- [ ] Configurar logs y monitoreo
- [ ] Configurar rate limiting
- [ ] Deshabilitar documentación pública (`/docs`, `/redoc`) si es necesario
- [ ] Configurar firewall para puertos 80/443/8000