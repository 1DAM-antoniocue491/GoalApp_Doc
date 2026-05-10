# Base de datos

La app utiliza una base de datos relacional para almacenar toda la información necesaria para la gestión de la plataforma, incluyendo usuarios, equipos, jugadores, partidos y eventos asociados a los encuentros deportivos.

El diseño de la base de datos sigue un modelo estructurado que permite mantener la **integridad de los datos**, facilitar las consultas y asegurar la escalabilidad del sistema a medida que aumenta el volumen de información.

La comunicación entre el backend de la aplicación y la base de datos se realiza mediante un **ORM (Object Relational Mapping)**, lo que permite trabajar con objetos de Python en lugar de consultas SQL directas.

***

### 1. Sistema Gestor de Base de Datos

El sistema utiliza **PostgreSQL** como sistema gestor de base de datos relacional (SGBD), optimizado para despliegues en Render.

Este gestor ha sido seleccionado por las siguientes razones:

* Alto rendimiento en aplicaciones web.
* Gran estabilidad y madurez tecnológica.
* Amplia compatibilidad con herramientas de desarrollo.
* Integración sencilla con aplicaciones desarrolladas en Python.

El uso de un sistema relacional permite organizar los datos en **tablas relacionadas mediante claves primarias y foráneas**, garantizando la consistencia de la información almacenada.

Además, el modelo relacional facilita la realización de consultas complejas necesarias para gestionar estadísticas deportivas, resultados de partidos y relaciones entre entidades como equipos, jugadores y competiciones.

***

### 2. Conexión desde el Backend

La conexión entre el backend y la base de datos se realiza mediante el ORM **SQLAlchemy**, que permite mapear las tablas de la base de datos a clases Python.

El backend está desarrollado utilizando el framework **FastAPI**, que utiliza dependencias para gestionar las sesiones de base de datos en cada petición.

El ORM se encarga de:

* establecer la conexión con la base de datos
* gestionar sesiones de consulta
* ejecutar operaciones CRUD
* mapear resultados a objetos Python

#### Ejemplo de configuración de conexión

La configuración de conexión y la creación de sesiones de base de datos se encuentran en `app/database/connection.py`.

```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker, declarative_base
from ..config import settings

# ============================================================
# CONFIGURACIÓN DE LA BASE DE DATOS
# ============================================================

# Motor de base de datos con configuración desde settings
engine = create_engine(
    settings.DATABASE_URL,
    echo=settings.DATABASE_ECHO,  
    pool_pre_ping=True,
    pool_recycle=3600,  # Reciclar conexiones cada hora
    pool_size=10,  # Número de conexiones en el pool
    max_overflow=20  # Conexiones adicionales si se agota el pool
)

# Crea la fábrica de sesiones
SessionLocal = sessionmaker(
    autocommit=False,
    autoflush=False,
    bind=engine
)

# Base para los modelos
Base = declarative_base()
```

En este módulo se definen los elementos principales de acceso a la base de datos:

* **engine**: motor de conexión con la base de datos
* **SessionLocal**: generador de sesiones para interactuar con la base de datos
* **Base**: clase base utilizada por los modelos ORM

Estas sesiones son utilizadas posteriormente por los distintos servicios y routers de la API para realizar operaciones sobre la base de datos.

***

### 3. Inicialización de la Base de Datos

Para facilitar la creación inicial de la base de datos, el proyecto incluye un **script SQL de inicialización** que permite generar la estructura básica de tablas y relaciones necesarias para el funcionamiento del sistema.

Este script se encuentra en el directorio:

```
app/database/init.sql
```

El archivo contiene las instrucciones SQL necesarias para crear las tablas principales del sistema dentro de **PostgreSQL**.

#### Ejemplo de creación de una tabla

```sql
CREATE TABLE roles (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50) NOT NULL
);
```

Este procedimiento permite:

* desplegar rápidamente la base de datos en un nuevo entorno
* mantener una estructura de datos consistente entre diferentes instalaciones
* facilitar el proceso de desarrollo y pruebas

El script puede ejecutarse directamente en el servidor de base de datos mediante herramientas de administración como el cliente de **psql** o mediante interfaces gráficas de gestión de bases de datos.
