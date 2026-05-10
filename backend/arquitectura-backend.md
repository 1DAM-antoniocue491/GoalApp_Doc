# Arquitectura backend

El backend de la aplicación está desarrollado utilizando el framework **FastAPI**, siguiendo una **arquitectura por capas** que separa claramente las responsabilidades de cada componente del sistema.

Este enfoque permite que el código sea **más mantenible, escalable y fácil de testear**, ya que cada capa se encarga de una función específica dentro de la aplicación.

La aplicación se estructura en tres capas principales:

* Capa de presentación (API / Routers)
* Capa de lógica de negocio (Services)
* Capa de acceso a datos (Models / ORM)

La comunicación entre capas sigue un flujo descendente donde cada capa interactúa únicamente con la inmediatamente inferior.

***

### 1. Arquitectura por Capas

El sistema sigue una arquitectura en capas para separar las responsabilidades de cada parte del backend.

```
Cliente (Web / Mobile)
        │
        ▼
Routers (API REST)
        │
        ▼
Services (Lógica de negocio)
        │
        ▼
Models (ORM)
        │
        ▼
Base de Datos
```

#### 1.1. Capa de Presentación (Routers)

La capa de presentación está implementada mediante **routers de FastAPI**, ubicados en `app/api/routers/`.

Su función es:

* Definir los endpoints de la API.
* Recibir las peticiones HTTP del cliente.
* Validar los datos de entrada mediante esquemas de **Pydantic**.
* Delegar la lógica de negocio a la capa de servicios.
* Formatear la respuesta que se devuelve al cliente.

Cada recurso de la API tiene su propio router.

Ejemplo de estructura:
```
app/api/routers/
├── auth.py
├── usuarios.py
├── equipos.py
├── jugadores.py
├── partidos.py
├── ligas.py
├── alineaciones.py
├── convocatorias.py
├── eventos.py
├── imagenes.py
├── invitaciones.py
├── notificaciones.py
├── public.py
├── roles.py
├── estadisticas.py
├── tokens_recuperacion.py
└── liga_configuracion.py
```

Ejemplo de endpoint:

```python
@router.post("/", response_model=JugadorResponse)
def crear_jugador(
    jugador: JugadorCreate,
    db: Session = Depends(get_db)
):
    return jugador_service.crear_jugador(db, jugador)
```

En este punto el router **no contiene lógica compleja**, únicamente gestiona la comunicación HTTP.

***

### 2. Capa de Servicios (Lógica de Negocio)

La capa de servicios contiene la **lógica de negocio de la aplicación**. Se encuentra ubicada en `app/api/services/`.

Aquí se implementan las reglas que determinan cómo se procesan los datos antes de almacenarlos o devolverlos al cliente.

Ejemplos de lógica de negocio:

* Validar que un usuario exista antes de crear un jugador.
* Comprobar que un partido pertenece a una liga válida.
* Validar permisos de un usuario.
* Gestionar operaciones complejas entre múltiples tablas.

Los servicios se organizan por dominio funcional:

```
app/api/services/
├── usuario_service.py
├── jugador_service.py
├── equipo_service.py
├── partido_service.py
├── auth_service.py
└── ... (demás servicios por dominio)
```

Ejemplo:

```python
def crear_jugador(db: Session, jugador: JugadorCreate):
    usuario = db.query(Usuario).filter(
        Usuario.id_usuario == jugador.id_usuario
    ).first()

    if not usuario:
        raise HTTPException(404, "Usuario no encontrado")

    db_jugador = Jugador(**jugador.model_dump())

    db.add(db_jugador)
    db.commit()
    db.refresh(db_jugador)

    return db_jugador
```

Esta capa permite que la lógica de negocio esté **desacoplada de la API**.

***

### 3. Capa de Datos (ORM)

La capa de datos está implementada mediante **SQLAlchemy**, que actúa como ORM (Object Relational Mapper). Los modelos se definen en `app/models/`.

Un ORM permite interactuar con la base de datos mediante objetos Python en lugar de escribir consultas SQL manualmente.

Cada modelo representa una tabla de la base de datos.

Ejemplo de modelo:

```python
class Jugador(Base):
    __tablename__ = "jugadores"

    id_jugador = Column(Integer, primary_key=True)
    id_usuario = Column(Integer, ForeignKey("usuarios.id_usuario"))
    id_equipo = Column(Integer, ForeignKey("equipos.id_equipo"))
    posicion = Column(String(50))
    dorsal = Column(Integer)
    activo = Column(Boolean, default=True)
```

Los modelos también definen:

* Relaciones entre tablas
* Tipos de datos
* Restricciones

***

### 4. Capa de Persistencia

La capa de persistencia corresponde a la base de datos relacional **PostgreSQL**, optimizada para despliegues en Render.

En ella se almacenan:

* Usuarios
* Equipos
* Ligas
* Jugadores
* Partidos
* Eventos
* Notificaciones

La comunicación entre la aplicación y la base de datos se realiza a través de **SQLAlchemy** mediante sesiones de base de datos gestionadas en `app/database/connection.py`.

***

### 5. Validación de Datos

La validación de datos se realiza mediante la librería **Pydantic**. Los esquemas se definen en `app/schemas/`.

Los esquemas definen:

* Qué datos acepta la API.
* Qué datos devuelve la API.
* Qué validaciones se deben aplicar.

Cada recurso dispone de varios esquemas:

| Tipo de Schema | Uso                  |
| -------------- | -------------------- |
| Base           | Campos comunes       |
| Create         | Crear recursos       |
| Update         | Actualizar recursos  |
| Response       | Respuestas de la API |

Ejemplo:

```python
class UsuarioCreate(BaseModel):
    nombre: str
    email: EmailStr
    contrasena: str
```

***

### 6. Sistema de Autenticación

El sistema de autenticación está basado en **JSON Web Token (JWT)**.

El flujo de autenticación funciona de la siguiente forma:

1. El usuario envía sus credenciales al endpoint `/auth/login`.
2. El servidor valida las credenciales.
3. Si son correctas, se genera un token JWT firmado.
4. El cliente almacena el token.
5. En cada petición protegida se envía el token en el header.

Ejemplo de header:

```
Authorization: Bearer <token>
```

El backend valida el token en cada petición protegida mediante dependencias de **FastAPI**.

***

### 7. Inyección de Dependencias

El sistema utiliza el mecanismo de **inyección de dependencias** de **FastAPI**.

Esto permite compartir funcionalidades comunes como:

* conexión a base de datos
* autenticación
* control de permisos

Ejemplo:

```python
def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()
```

Uso en endpoint:

```python
@router.get("/me")
def obtener_usuario(
    db: Session = Depends(get_db),
    user = Depends(get_current_user)
):
    return user
```

Esto mejora:

* reutilización de código
* separación de responsabilidades
* testabilidad
