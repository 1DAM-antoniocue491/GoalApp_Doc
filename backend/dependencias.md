# Dependencias

Este documento describe las librerías y paquetes Python utilizados en el backend de GoalApp, explicando su propósito y configuración.

***

### 1. Lista de Dependencias

El archivo `requirements.txt` contiene todas las dependencias necesarias:

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

### 2. Dependencias Principales

#### FastAPI

```txt
fastapi
```

**Propósito:** Framework web moderno y de alto rendimiento para construir APIs con Python.

**Características:**
- Documentación automática (Swagger/OpenAPI)
- Validación de datos integrada
- Sistema de dependencias potente
- Soporte para async/await
- Type hints nativos

**Uso en el proyecto:**
- Definición de routers y endpoints
- Sistema de dependencias (`Depends`)
- Validación automática con Pydantic
- Generación de documentación interactiva

```python
from fastapi import FastAPI, Depends, HTTPException

app = FastAPI(title="Liga Amateur App")

@app.get("/usuarios/")
def listar_usuarios(db: Session = Depends(get_db)):
    return obtener_usuarios(db)
```

**Documentación:** https://fastapi.tiangolo.com/

***

#### Uvicorn

```txt
uvicorn[standard]
```

**Propósito:** Servidor ASGI de alto rendimiento para ejecutar aplicaciones FastAPI.

**Características:**
- Servidor ASGI ligero y rápido
- Soporte para HTTP/2 y WebSockets
- Auto-reload en desarrollo
- Compatible con múltiples workers

**Uso en el proyecto:**
- Servidor de desarrollo con `--reload`
- Servidor de producción con Gunicorn

```bash
# Desarrollo
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000

# Producción
gunicorn app.main:app --workers 4 --worker-class uvicorn.workers.UvicornWorker
```

**Documentación:** https://www.uvicorn.org/

***

#### SQLAlchemy

```txt
sqlalchemy
```

**Propósito:** ORM (Object Relational Mapper) para interactuar con bases de datos relacionales.

**Características:**
- Mapeo objeto-relacional
- Consultas con expresiones Python
- Soporte para múltiples bases de datos
- Sistema de sesiones para manejo de transacciones
- Migraciones con Alembic

**Uso en el proyecto:**
- Definición de modelos (tablas)
- Consultas a la base de datos
- Gestión de sesiones
- Relaciones entre entidades

```python
from sqlalchemy import Column, Integer, String, ForeignKey
from sqlalchemy.orm import relationship
from app.database.connection import Base

class Usuario(Base):
    __tablename__ = "usuarios"

    id_usuario = Column(Integer, primary_key=True)
    nombre = Column(String(100))
    email = Column(String(100), unique=True)
    contrasena = Column(String(255))

    roles = relationship("Rol", secondary="usuario_rol", back_populates="usuarios")
```

**Documentación:** https://docs.sqlalchemy.org/

***

#### PyMySQL

```txt
pymysql
```

**Propósito:** Driver de MySQL para Python, necesario para que SQLAlchemy se conecte a MySQL.

**Características:**
- Implementación pura de Python
- Compatible con MySQL 5.5+
- Soporte para prepared statements
- Conexiones seguras

**Uso en el proyecto:**
- Conector MySQL en la URL de conexión

```python
# Formato de la URL de conexión
DATABASE_URL = "mysql+pymysql://usuario:password@localhost:3306/futbol_app"
```

**Documentación:** https://pymysql.readthedocs.io/

***

#### Alembic

```txt
alembic
```

**Propósito:** Herramienta de migración de base de datos para SQLAlchemy.

**Características:**
- Control de versiones del esquema de base de datos
- Migraciones automáticas desde modelos
- Rollback de migraciones
- Historial de cambios

**Uso en el proyecto:**
- Migraciones de esquema en producción
- Control de versiones de la base de datos

```bash
# Inicializar Alembic
alembic init alembic

# Crear migración
alembic revision --autogenerate -m "Añadir tabla usuarios"

# Aplicar migraciones
alembic upgrade head

# Rollback
alembic downgrade -1
```

**Documentación:** https://alembic.sqlalchemy.org/

***

#### Python-dotenv

```txt
python-dotenv
```

**Propósito:** Cargar variables de entorno desde archivos `.env`.

**Características:**
- Lectura automática de `.env`
- Separación de configuración y código
- Diferentes configuraciones por entorno

**Uso en el proyecto:**
- Carga de configuración sensible
- Configuración por entorno (dev, prod)

```python
from dotenv import load_dotenv

load_dotenv()  # Carga variables desde .env

import os
SECRET_KEY = os.getenv("SECRET_KEY")
```

**Documentación:** https://github.com/theskumar/python-dotenv

***

### 3. Validación y Configuración

#### Pydantic

```txt
pydantic[email]
pydantic-settings
```

**Propósito:** Validación de datos y gestión de configuración con type hints.

**Características:**
- Validación automática de tipos
- Serialización JSON
- Validadores personalizados
- Soporte para emails (`pydantic[email]`)
- Gestión de settings (`pydantic-settings`)

**Uso en el proyecto:**
- Esquemas de request/response
- Validación de datos de entrada
- Configuración de la aplicación

```python
from pydantic import BaseModel, EmailStr, validator
from pydantic_settings import BaseSettings

# Esquemas
class UsuarioCreate(BaseModel):
    nombre: str
    email: EmailStr
    contrasena: str

    @validator('contrasena')
    def validar_contrasena(cls, v):
        if len(v) < 8:
            raise ValueError('Mínimo 8 caracteres')
        return v

# Configuración
class Settings(BaseSettings):
    DATABASE_URL: str
    SECRET_KEY: str

    model_config = {"env_file": ".env"}

settings = Settings()
```

**Documentación:** https://docs.pydantic.dev/

***

### 4. Seguridad

#### Python-jose

```txt
python-jose
```

**Propósito:** Implementación de JWT (JSON Web Tokens) y algoritmos criptográficos.

**Características:**
- Generación y validación de JWT
- Soporte para múltiples algoritmos (HS256, RS256, etc.)
- Codificación/decodificación de claims

**Uso en el proyecto:**
- Generación de tokens de acceso
- Validación de tokens en cada petición
- Expiración de sesiones

```python
from jose import jwt, JWTError
from datetime import datetime, timedelta

def create_access_token(data: dict):
    to_encode = data.copy()
    expire = datetime.utcnow() + timedelta(minutes=60)
    to_encode.update({"exp": expire})
    return jwt.encode(to_encode, SECRET_KEY, algorithm="HS256")

def verify_token(token: str):
    try:
        payload = jwt.decode(token, SECRET_KEY, algorithms=["HS256"])
        return payload
    except JWTError:
        return None
```

**Documentación:** https://github.com/mpdavis/python-jose

***

#### Passlib

```txt
passlib[bcrypt]
```

**Propósito:** Hashing de contraseñas con múltiples algoritmos.

**Características:**
- Soporte para bcrypt, argon2, PBKDF2
- Verificación de contraseñas
- Migración entre algoritmos
- Generación de salt automático

**Uso en el proyecto:**
- Hash de contraseñas al registrar
- Verificación en el login

```python
from passlib.context import CryptContext

pwd_context = CryptContext(schemes=["bcrypt"], deprecated="auto")

# Hash de contraseña
hashed = pwd_context.hash("contrasena123")

# Verificación
is_valid = pwd_context.verify("contrasena123", hashed)
```

**Documentación:** https://passlib.readthedocs.io/

***

#### Cryptography

```txt
cryptography
```

**Propósito:** Funciones criptográficas primitivas y de alto nivel.

**Características:**
- Cifrado simétrico y asimétrico
- Funciones hash
- Generación de números aleatorios
- Certificados X.509

**Uso en el proyecto:**
- Dependencia de python-jose para JWT
- Soporte criptográfico en passlib

**Documentación:** https://cryptography.io/

***

### 5. Utilidades

#### Python-multipart

```txt
python-multipart
```

**Propósito:** Manejo de formularios multipart/form-data.

**Características:**
- Parsing de formularios
- Upload de archivos
- Compatible con FastAPI

**Uso en el proyecto:**
- Login con OAuth2PasswordRequestForm
- Upload de archivos (escudos, imágenes)

```python
from fastapi import File, UploadFile

@router.post("/upload/")
async def upload_file(file: UploadFile = File(...)):
    contents = await file.read()
    # Procesar archivo
    return {"filename": file.filename}
```

**Documentación:** https://andrew-d.github.io/python-multipart/

***

### 6. Dependencias de Desarrollo

#### Dependencias opcionales para desarrollo

```txt
# Testing
pytest
pytest-cov
httpx

# Calidad de código
black
flake8
isort
mypy

# Documentación
mkdocs
mkdocs-material
```

**Pytest:** Framework de testing

```bash
pytest tests/
pytest --cov=app tests/
```

**Black:** Formateador de código

```bash
black app/
```

**Flake8:** Linter

```bash
flake8 app/
```

***

### 7. Instalación y Gestión

#### Instalar todas las dependencias

```bash
pip install -r requirements.txt
```

#### Instalar dependencias de desarrollo

```bash
pip install -r requirements-dev.txt
```

#### Actualizar dependencias

```bash
pip install --upgrade -r requirements.txt
```

#### Verificar dependencias instaladas

```bash
pip list
pip freeze
```

***

### 8. Versiones Recomendadas

| Paquete | Versión recomendada | Notas |
|---------|---------------------|-------|
| fastapi | >= 0.100.0 | Type hints mejorados |
| uvicorn | >= 0.23.0 | Mejoras de rendimiento |
| sqlalchemy | >= 2.0.0 | Sintaxis 2.0 |
| pydantic | >= 2.0.0 | Pydantic V2 |
| python-jose | >= 3.3.0 | Soporte completo JWT |
| passlib | >= 1.7.4 | Última estable |

**Fijar versiones en requirements.txt:**

```txt
fastapi==0.109.0
uvicorn[standard]==0.27.0
sqlalchemy==2.0.25
```

***

### 9. Resumen de Dependencias

| Categoría | Paquete | Propósito |
|-----------|---------|-----------|
| **Framework** | fastapi | API REST |
| **Servidor** | uvicorn | Servidor ASGI |
| **ORM** | sqlalchemy | Mapeo objeto-relacional |
| **Driver** | pymysql | Conector MySQL |
| **Migraciones** | alembic | Control de versiones DB |
| **Configuración** | python-dotenv | Variables de entorno |
| **Validación** | pydantic | Validación de datos |
| **Autenticación** | python-jose | JWT tokens |
| **Hashing** | passlib | Contraseñas |
| **Criptografía** | cryptography | Soporte criptográfico |
| **Formularios** | python-multipart | Upload y forms |

***

### 10. Estructura de requirements.txt

```txt
# Framework y servidor
fastapi
uvicorn[standard]

# Base de datos
sqlalchemy
pymysql
alembic

# Configuración
python-dotenv
pydantic[email]
pydantic-settings

# Seguridad
python-jose
passlib[bcrypt]
cryptography

# Utilidades
python-multipart
```

**Organización recomendada:**
1. Framework y servidor
2. Base de datos
3. Configuración
4. Seguridad
5. Utilidades adicionales