# Estructura del proyecto

El backend de este proyecto está desarrollado utilizando FastAPI como framework principal para la construcción de la API REST.

La arquitectura sigue un **modelo por capas**, separando responsabilidades para facilitar el mantenimiento, la escalabilidad y la claridad del código.

Las principales tecnologías utilizadas son:

* [FastAPI](https://fastapi.tiangolo.com/) para la construcción de la API.
* [SQLAlchemy](https://docs.sqlalchemy.org/en/20/) como ORM para la interacción con la base de datos.
* [Pydantic](https://docs.pydantic.dev/latest/) para la validación de datos.
* [JSON Web Token](https://www.ibm.com/docs/es/cics-ts/6.x?topic=cics-json-web-token-jwt) para el sistema de autenticación.
* [MySQL](https://www.mysql.com/) como sistema gestor de base de datos.

La estructura principal del proyecto es la siguiente:

```
backend/
│
├── app/
│   │
│   ├── core/
│   │   ├── config.py
│   │   └── security.py
│   │
│   ├── database/
│   │   ├── database.py
│   │   └── init.sql
│   │
│   ├── models/
│   │   ├── user.py
│   │   ├── team.py
│   │   ├── player.py
│   │   ├── match.py
│   │   └── event.py
│   │
│   ├── schemas/
│   │   ├── user_schema.py
│   │   ├── team_schema.py
│   │   └── match_schema.py
│   │
│   ├── services/
│   │   ├── user_service.py
│   │   ├── team_service.py
│   │   └── match_service.py
│   │
│   ├── routers/
│   │   ├── auth_router.py
│   │   ├── user_router.py
│   │   └── team_router.py
│   │
│   └── main.py
│
├── requirements.txt
└── README.md
```

***

### 1. Directorio `core`

Este directorio contiene la **configuración global de la aplicación** y los elementos relacionados con la seguridad.

#### Ejemplo: `security.py`

Aquí se implementa la generación de tokens de autenticación mediante JSON Web Token.

```python
from datetime import datetime, timedelta
from jose import jwt

SECRET_KEY = "secret"
ALGORITHM = "HS256"

def create_access_token(data: dict, expires_delta: timedelta = None):
    to_encode = data.copy()

    expire = datetime.utcnow() + (expires_delta or timedelta(minutes=30))
    to_encode.update({"exp": expire})

    encoded_jwt = jwt.encode(to_encode, SECRET_KEY, algorithm=ALGORITHM)

    return encoded_jwt
```

***

### 2. Directorio `database`

Contiene la configuración de conexión a la base de datos y scripts de inicialización.

#### Ejemplo: `database.py`

Configuración de la conexión con la base de datos mediante SQLAlchemy.

```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker, declarative_base

DATABASE_URL = "mysql+pymysql://user:password@localhost/liga_amateur"

engine = create_engine(DATABASE_URL)

SessionLocal = sessionmaker(
    autocommit=False,
    autoflush=False,
    bind=engine
)

Base = declarative_base()
```

***

#### Ejemplo: `init.sql`

Script de creación inicial de tablas en MySQL.

```sql
CREATE TABLE roles (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50) NOT NULL
);

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL,
    password VARCHAR(255) NOT NULL,
    role_id INT,
    FOREIGN KEY (role_id) REFERENCES roles(id)
);
```

***

### 3. Directorio `models`

Define las **entidades de la base de datos** utilizando el ORM de SQLAlchemy.

Cada modelo representa una tabla de la base de datos.

#### Ejemplo: `user.py`

```python
from sqlalchemy import Column, Integer, String, ForeignKey
from sqlalchemy.orm import relationship
from app.database.database import Base

class User(Base):
    __tablename__ = "users"

    id = Column(Integer, primary_key=True, index=True)
    username = Column(String(50))
    email = Column(String(100))
    password = Column(String(255))

    role_id = Column(Integer, ForeignKey("roles.id"))

    role = relationship("Role")
```

***

### 4. Directorio `schemas`

Define los **esquemas de validación** mediante Pydantic.

Estos esquemas se utilizan para:

* validar los datos de entrada
* definir el formato de salida de la API

#### Ejemplo: `user_schema.py`

```python
from pydantic import BaseModel

class UserCreate(BaseModel):
    username: str
    email: str
    password: str


class UserResponse(BaseModel):
    id: int
    username: str
    email: str
```

***

### 5. Directorio `services`

Contiene la **lógica de negocio del sistema**.

Los servicios gestionan las operaciones sobre los modelos de datos.

#### Ejemplo: `user_service.py`

```python
from sqlalchemy.orm import Session
from app.models.user import User

def get_users(db: Session):
    return db.query(User).all()


def create_user(db: Session, user_data):
    user = User(**user_data.dict())
    db.add(user)
    db.commit()
    db.refresh(user)
    return user
```

***

### 6. Directorio `routers`

Define los **endpoints de la API REST** mediante FastAPI.

Cada router agrupa las rutas relacionadas con una entidad concreta.

#### Ejemplo: `user_router.py`

```python
from fastapi import APIRouter, Depends
from sqlalchemy.orm import Session

from app.database.database import SessionLocal
from app.services.user_service import get_users

router = APIRouter(prefix="/users", tags=["Users"])


def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()


@router.get("/")
def read_users(db: Session = Depends(get_db)):
    return get_users(db)
```

***

### 7. Archivo `main.py`

Archivo principal donde se crea la aplicación de FastAPI y se registran los routers.

#### Ejemplo:

```python
from fastapi import FastAPI

from app.routers import user_router
from app.routers import auth_router

app = FastAPI()

app.include_router(auth_router.router)
app.include_router(user_router.router)
```
