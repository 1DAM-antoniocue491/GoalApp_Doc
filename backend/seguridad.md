# Seguridad

Este documento describe las medidas de seguridad implementadas en el backend de GoalApp y las recomendaciones para un despliegue seguro en producción.

***

### 1. Autenticación y Autorización

#### Sistema JWT

La autenticación se basa en **JSON Web Tokens (JWT)** con las siguientes características:

| Característica | Implementación |
|----------------|----------------|
| Algoritmo de firma | HS256 (HMAC con SHA-256) |
| Tiempo de expiración | Configurable vía `ACCESS_TOKEN_EXPIRE_MINUTES` en `.env` (valor real: 30 días en ejemplo) |
| Clave secreta | 64 bytes generados con `secrets.token_urlsafe(64)` |
| Payload mínimo | Solo contiene `sub` (ID del usuario) |

#### Hashing de Contraseñas

Las contraseñas se almacenan hasheadas usando **bcrypt**:

```python
from passlib.context import CryptContext

pwd_context = CryptContext(schemes=["bcrypt"], deprecated="auto")

# Hash de contraseña
hashed = pwd_context.hash(contrasena_plana)

# Verificación
pwd_context.verify(contrasena_plana, hashed)
```

**Características de bcrypt:**
- Salt aleatorio automático
- Costo computacional configurable (work factor)
- Resistente a ataques de rainbow tables
- Resistente a ataques de fuerza bruta

#### Sistema de Roles (RBAC)

El sistema implementa **Role-Based Access Control**:

| Rol | Permisos |
|-----|----------|
| `admin` | Acceso total al sistema |
| `coach` | Gestión de su equipo y alineaciones |
| `delegate` | Registrar eventos de partidos asignados |
| `player` | Ver su propia información y estadísticas |
| `viewer` | Ver información pública |

```python
# Ejemplo de protección por rol
@router.post("/", dependencies=[Depends(require_role("admin"))])
def crear_recurso(...):
    pass
```

***

### 2. Validación de Datos

#### Pydantic Schemas

Toda entrada de datos se valida mediante **Pydantic**:

```python
from pydantic import BaseModel, EmailStr, validator

class UsuarioCreate(BaseModel):
    nombre: str
    email: EmailStr              # Valida formato de email
    contrasena: str

    @validator('contrasena')
    def validar_contrasena(cls, v):
        if len(v) < 8:
            raise ValueError('La contraseña debe tener al menos 8 caracteres')
        return v
```

**Validaciones automáticas:**
- Tipos de datos (int, str, float, bool)
- Formato de emails (`EmailStr`)
- Fechas y horas (`datetime`)
- Enumeraciones para valores permitidos
- Campos obligatorios vs opcionales

#### Sanitización de Entrada

SQLAlchemy ORM previene **inyección SQL** automáticamente:

```python
# ✅ Seguro - SQLAlchemy parametriza las consultas
usuario = db.query(Usuario).filter(Usuario.email == email).first()

# ❌ Nunca hacer esto (vulnerable a SQL injection)
# db.execute(f"SELECT * FROM usuarios WHERE email = '{email}'")
```

***

### 3. CORS (Cross-Origin Resource Sharing)

#### Configuración Actual

La configuración se gestiona dinámicamente mediante `settings.get_cors_origins_list()` en el middleware de FastAPI.

```python
# En app/main.py
app.add_middleware(
    CORSMiddleware,
    allow_origins=settings.get_cors_origins_list(),
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
```

#### Recomendaciones para Producción

```python
# Configuración estricta para producción
ALLOWED_ORIGINS = [
    "https://goalapp.com",
    "https://www.goalapp.com",
    "https://api.goalapp.com",
]
```

| Header | Valor recomendado |
|--------|-------------------|
| `Access-Control-Allow-Origin` | Solo dominios específicos |
| `Access-Control-Allow-Credentials` | `true` si se usan cookies |
| `Access-Control-Allow-Methods` | Solo métodos necesarios |
| `Access-Control-Allow-Headers` | Solo headers necesarios |

***

### 4. Headers de Seguridad

#### Headers Recomendados

Para producción, añadir estos headers con un proxy (Nginx) o middleware:

```python
# Middleware de headers de seguridad
@app.middleware("http")
async def add_security_headers(request: Request, call_next):
    response = await call_next(request)

    # Previene clickjacking
    response.headers["X-Frame-Options"] = "DENY"

    # Previene MIME type sniffing
    response.headers["X-Content-Type-Options"] = "nosniff"

    # Protección XSS
    response.headers["X-XSS-Protection"] = "1; mode=block"

    # Content Security Policy
    response.headers["Content-Security-Policy"] = "default-src 'self'"

    # No exponer información del servidor
    response.headers["X-Powered-By"] = ""

    return response
```

#### En Nginx

```nginx
server {
    # ... configuración ...

    add_header X-Frame-Options "DENY" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header X-XSS-Protection "1; mode=block" always;
    add_header Content-Security-Policy "default-src 'self'" always;
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
}
```

***

### 5. Variables de Entorno

#### Archivo .env

El archivo `. la env` contiene información sensible y **NUNCA** debe subirse al repositorio:

```gitignore
# .gitignore
.env
*.env.local
*.env.production
```

#### Variables Sensibles

| Variable | Riesgo si se expone |
|----------|---------------------|
| `SECRET_KEY` | Permite falsificar tokens JWT |
| `DATABASE_URL` | Acceso completo a la base de datos |
| Credenciales DB | Acceso directo a datos |

#### Generación de SECRET_KEY

```bash
# Generar clave segura de 64 bytes
python -c "import secrets; print(secrets.token_urlsafe(64))"
```

**⚠️ Nunca usar valores por defecto en producción**

***

### 6. Rate Limiting

#### Implementación Recomendada

Para prevenir ataques de fuerza bruta y abuso de la API:

```bash
# Instalar slowapi
pip install slowapi
```

```python
from slowapi import Limiter
from slowapi.util import get_remote_address

limiter = Limiter(key_func=get_remote_address)

# Limitar intentos de login
@limiter.limit("5/minute")
@router.post("/auth/login")
def login(...):
    pass
```

#### Límites Recomendados

| Endpoint | Límite | Razón |
|----------|--------|-------|
| `/auth/login` | 5/minuto | Prevenir fuerza bruta |
| `/auth/refresh` | 10/minuto | Prevenir abuso |
| `/usuarios/` (POST) | 5/hora | Prevenir spam de registros |
| API general | 100/minuto | Uso normal |

***

### 7. HTTPS Obligatorio

#### En Desarrollo

```
http://localhost:8000  # Aceptable solo en desarrollo local
```

#### En Producción

```
https://api.goalapp.com  # Obligatorio
```

**Razones:**
- Los tokens JWT viajan en headers (Authorization: Bearer)
- Sin HTTPS, los tokens pueden ser interceptados
- Las credenciales de login viajan en texto plano

#### Configurar HTTPS con Let's Encrypt

```bash
# Instalar Certbot
sudo apt install certbot python3-certbot-nginx

# Obtener certificado
sudo certbot --nginx -d api.goalapp.com

# Renovación automática
sudo certbot renew --dry-run
```

***

### 8. Base de Datos

#### Usuario Dedicado

No usar `root` en producción:

```sql
-- Crear usuario con permisos limitados
CREATE USER 'goalapp_user'@'localhost' IDENTIFIED BY 'contrasena_segura';
GRANT SELECT, INSERT, UPDATE, DELETE ON futbol_app.* TO 'goalapp_user'@'localhost';
FLUSH PRIVILEGES;
```

#### Conexión Segura

```env
# URL con usuario dedicado
DATABASE_URL=postgresql+psycopg2://goalapp_user:contrasena_segura@localhost:5432/futbol_app
```

#### Backup Automático

```bash
# Script de backup diario
pg_dump -U goalapp_user futbol_app > backup_$(date +%Y%m%d).sql
```

***

### 9. Logs y Auditoría

#### Qué Registrar

| Evento | Información |
|--------|-------------|
| Login exitoso | Usuario, IP, timestamp |
| Login fallido | Email intentado, IP, timestamp |
| Accesos denegados | Usuario, recurso, IP |
| Cambios críticos | Usuario, entidad, acción, timestamp |

#### Ejemplo de Log

```python
import logging

logger = logging.getLogger(__name__)

@router.post("/auth/login")
def login(...):
    try:
        usuario = autenticar_usuario(db, email, password)
        logger.info(f"Login exitoso: {email} desde {request.client.host}")
    except:
        logger.warning(f"Login fallido: {email} desde {request.client.host}")
```

#### No Registrar

- Contraseñas (ni en texto plano ni hasheadas)
- Tokens JWT completos
- Datos sensibles de usuarios

***

### 10. Vulnerabilidades Conocidas

Consultar el archivo `ERRORES_SEGURIDAD_AUTENTICACION.md` para el análisis detallado de:

| Vulnerabilidad | Severidad | Estado |
|----------------|-----------|--------|
| Refresh token sin validación de expiración | ALTA | Documentado |
| Sin distinción access/refresh tokens | MEDIA | Documentado |
| Sin mecanismo de revocación de tokens | MEDIA | Documentado |
| Sin rate limiting en login | MEDIA | Recomendación |
| `datetime.utcnow()` deprecado | BAJA | Documentado |
