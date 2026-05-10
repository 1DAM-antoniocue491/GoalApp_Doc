# Despliegue backend

Esta guía explica cómo desplegar el backend de GoalApp en diferentes entornos, utilizando Render como plataforma principal de despliegue.

---

## 1. Requisitos Previos

### Software Necesario

|Requisito|Versión|Descripción|
|---|---|---|
|Python|3.10+|Intérprete de Python|
|PostgreSQL|14+|Base de datos relacional|
|pip|21+|Gestor de paquetes Python|
|Git|2.x|Control de versiones|

### Servicios Necesarios

| Servicio                     | Descripción              |
| ---------------------------- | ------------------------ |
| [Render](https://render.com) | Hosting del backend      |
| PostgreSQL                   | Base de datos principal  |
| [GitHub](https://github.com) | Repositorio del proyecto |

---

## 2. Configuración del Entorno

### Clonar el repositorio

```
git clone https://github.com/1DAM-antoniocue491/GoalApp_Backend
```

### Crear entorno virtual

**Windows (PowerShell):**

```
python -m venv .venv.\.venv\Scripts\Activate.ps1
```

**Linux/Mac:**

```
python -m venv .venvsource .venv/bin/activate
```

### Instalar dependencias

```
pip install -r requirements.txt
```

### Contenido de requirements.txt

```
fastapiuvicorn[standard]sqlalchemypsycopg2-binaryalembicpython-dotenvpydantic[email]pydantic-settingspython-josepasslib[bcrypt]python-multipartcryptographygunicorn
```

---

## 3. Variables de Entorno

### Crear archivo .env

```
cp .env.example .env
```

### Configuración completa (.env)

```
# ============================================================# CONFIGURACIÓN DE LA BASE DE DATOS# ============================================================DATABASE_URL=postgresql+psycopg2://usuario:password@localhost:5432/goalappDATABASE_ECHO=True# ============================================================# CONFIGURACIÓN DE SEGURIDAD JWT# ============================================================SECRET_KEY=tu_clave_secreta_aqui_cambiarALGORITHM=HS256ACCESS_TOKEN_EXPIRE_MINUTES=60# ============================================================# CONFIGURACIÓN DE LA APLICACIÓN# ============================================================APP_NAME=Liga Amateur AppAPI_VERSION=v1ENVIRONMENT=developmentPORT=8000HOST=0.0.0.0# ============================================================# CONFIGURACIÓN DE CORS# ============================================================CORS_ORIGINS=http://localhost:3000,http://localhost:5173,http://localhost:8081# ============================================================# CONFIGURACIÓN DE LOGGING# ============================================================LOG_LEVEL=INFO
```

### Descripción de Variables

|Variable|Descripción|Ejemplo|
|---|---|---|
|`DATABASE_URL`|URL de conexión a PostgreSQL|`postgresql+psycopg2://user:pass@host:5432/db`|
|`DATABASE_ECHO`|Mostrar SQL en consola|`True` o `False`|
|`SECRET_KEY`|Clave para firmar JWT|Generar con `secrets.token_urlsafe(64)`|
|`ALGORITHM`|Algoritmo JWT|`HS256`|
|`ACCESS_TOKEN_EXPIRE_MINUTES`|Duración del token|`60`|
|`ENVIRONMENT`|Entorno actual|`development` o `production`|
|`CORS_ORIGINS`|Orígenes permitidos|URLs separadas por coma|

---

## 4. Configuración de Base de Datos PostgreSQL

### Crear base de datos

```
CREATE DATABASE goalapp;
```

### Inicializar tablas

El backend crea automáticamente las tablas mediante SQLAlchemy:

```
Base.metadata.create_all(bind=engine)
```

### Ejecutar migraciones con Alembic

```
alembic upgrade head
```

---

## 5. Ejecución en Desarrollo

### Iniciar el servidor

```
uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

### Verificar funcionamiento

```
curl http://localhost:8000/health
```

### Documentación interactiva

- Swagger UI: `http://localhost:8000/docs`
- ReDoc: `http://localhost:8000/redoc`

---

## 6. Despliegue en Render

### Crear cuenta en Render

Acceder a:

[Render](https://render.com?utm_source=chatgpt.com)

### Crear servicio Web Service

1. Entrar en Dashboard
2. Pulsar **New +**
3. Seleccionar **Web Service**
4. Conectar repositorio de [GitHub](https://github.com?utm_source=chatgpt.com)
5. Seleccionar el repositorio de GoalApp

### Configuración del servicio

|Campo|Valor|
|---|---|
|Name|`goalapp-backend`|
|Environment|`Python`|
|Build Command|`pip install -r requirements.txt`|
|Start Command|`gunicorn app.main:app -k uvicorn.workers.UvicornWorker`|
|Root Directory|`backend`|

### Variables de entorno en Render

En la sección **Environment Variables** añadir:

```
DATABASE_URL=postgresql+psycopg2://...SECRET_KEY=...ALGORITHM=HS256ACCESS_TOKEN_EXPIRE_MINUTES=60APP_NAME=Liga Amateur AppAPI_VERSION=v1ENVIRONMENT=productionDATABASE_ECHO=FalseLOG_LEVEL=INFO
```

### Crear base de datos PostgreSQL en Render

1. Pulsar **New +**
2. Seleccionar **PostgreSQL**
3. Configurar:
    - Database Name: `goalapp-db`
    - User: automático
    - Región: misma que el backend

Render generará automáticamente la URL de conexión PostgreSQL.

---

## 7. Configuración de Producción

### Comando recomendado

```
gunicorn app.main:app \    --worker-class uvicorn.workers.UvicornWorker \    --workers 4 \    --bind 0.0.0.0:8000
```

### Configuración recomendada

|Parámetro|Valor|
|---|---|
|Workers|4|
|Timeout|120|
|Keep Alive|5|

---

## 8. Verificación del Despliegue

### Health Check

```
curl https://tu-backend.onrender.com/health
```

### Verificar API

```
curl https://tu-backend.onrender.com/api/v1/ligas/
```

### Verificar autenticación

```
curl -X POST https://tu-backend.onrender.com/api/v1/auth/login \    -H "Content-Type: application/x-www-form-urlencoded" \    -d "username=admin@email.com&password=password123"
```

---

## 9. Logs y Monitoreo

### Ver logs en Render

1. Entrar en el servicio
2. Ir a la pestaña **Logs**

### Niveles de logging

|Nivel|Uso|
|---|---|
|DEBUG|Desarrollo|
|INFO|Operaciones normales|
|WARNING|Advertencias|
|ERROR|Errores importantes|

---

## 10. Solución de Problemas Comunes

### Error de conexión a PostgreSQL

```
sqlalchemy.exc.OperationalError
```

**Solución:**

- Verificar `DATABASE_URL`
- Comprobar que PostgreSQL esté activo
- Revisar credenciales

### Error de CORS

```
Blocked by CORS policy
```

**Solución:**

- Añadir frontend a `CORS_ORIGINS`
- Verificar middleware CORS

### Error de módulos

```
ModuleNotFoundError: No module named 'app'
```

**Solución:**

- Verificar `Root Directory`
- Confirmar que Render apunta a `backend/`

---

## 11. Despliegue Automático

Render realiza despliegues automáticos cada vez que se hace push a la rama configurada del repositorio.

Flujo recomendado:

```
git add .git commit -m "Nuevo cambio"git push origin main
```

Después del push, Render reconstruirá y desplegará automáticamente el backend.