# Estructura del Proyecto Backend

El backend de GoalApp está desarrollado con **FastAPI**, implementando una arquitectura modular por capas que separa el transporte (API), la lógica de negocio (Servicios) y la persistencia (Modelos).

### Tecnologías Principales
- **Framework**: [FastAPI](https://fastapi.tiangolo.com/)
- **ORM**: [SQLAlchemy](https://docs.sqlalchemy.org/en/20/)
- **Validación**: [Pydantic](https://docs.pydantic.dev/latest/)
- **Base de Datos**: PostgreSQL (via Supabase)
- **Autenticación**: JSON Web Tokens (JWT)

---

### 📂 Mapa de Directorios Real

La estructura actual del proyecto se organiza de la siguiente manera:

```
GoalApp_Backend/
├── app/
│   ├── api/
│   │   ├── routers/        # Endpoints de la API (Transporte)
│   │   │   ├── auth.py
│   │   │   ├── usuarios.py
│   │   │   ├── ligas.py
│   │   │   ├── equipos.py
│   │   │   ├── jugadores.py
│   │   │   ├── partidos.py
│   │   │   ├── alineaciones.py
│   │   │   ├── convocatorias.py
│   │   │   ├── eventos.py
│   │   │   ├── notificaciones.py
│   │   │   ├── invitaciones.py
│   │   │   ├── imagenes.py
│   │   │   ├── public.py
│   │   │   └── ...
│   │   ├── services/       # Lógica de negocio y reglas
│   │   │   ├── auth_service.py
│   │   │   ├── liga_service.py
│   │   │   ├── email_service.py
│   │   │   └── ...
│   │   └── dependencies.py # Inyección de dependencias (get_db, get_user)
│   │
│   ├── models/            # Definiciones de tablas SQLAlchemy
│   │   ├── usuario.py
│   │   ├── liga.py
│   │   ├── partido.py
│   │   └── ...
│   │
│   ├── schemas/           # DTOs y validaciones Pydantic
│   │   ├── auth.py
│   │   ├── usuario.py
│   │   ├── partido.py
│   │   └── ...
│   │
│   ├── database/          # Conexión y configuración de DB
│   │   └── connection.py
│   │
│   ├── templates/        # Plantillas HTML para emails
│   │   └── emails/
│   │
│   └── main.py            # Punto de entrada de la aplicación
│
├── alembic/               # Control de versiones de la DB
├── migrations/            # Scripts de migración SQL
├── scripts/                # Scripts de utilidad y setup
├── tests/                 # Pruebas unitarias e integración
└── requirements.txt       # Dependencias del proyecto
```

---

### 🛠️ Descripción de Componentes

#### 1. Capa de Presentación (`app/api/routers/`)
Define los endpoints REST. Su única responsabilidad es recibir la petición, validar los datos mediante los esquemas de Pydantic y llamar al servicio correspondiente. No contiene lógica de negocio compleja.

#### 2. Capa de Servicios (`app/api/services/`)
Es el corazón de la aplicación. Aquí se implementan las reglas de negocio, validaciones cruzadas entre entidades y la orquestación de llamadas a la base de datos.

#### 3. Capa de Modelos (`app/models/`)
Define la estructura de la base de datos PostgreSQL mediante clases de SQLAlchemy. Gestiona las relaciones entre entidades (1:N, N:N) y las restricciones de integridad.

#### 4. Esquemas de Validación (`app/schemas/`)
Utiliza Pydantic para asegurar que los datos que entran y salen de la API sean correctos. Se dividen generalmente en:
- `Create`: Datos requeridos para crear un recurso.
- `Update`: Datos opcionales para actualizar.
- `Response`: Formato de salida filtrado para el cliente.

#### 5. Persistencia y Configuración
- **`app/database/connection.py`**: Gestiona la sesión de SQLAlchemy y la conexión al pool de Supabase.
- **`app/main.py`**: Instancia la aplicación FastAPI e integra todos los routers.
- **`alembic/`**: Permite evolucionar el esquema de la base de datos sin perder datos.
