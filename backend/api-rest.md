# Api REST

La API REST del backend está desarrollada con **FastAPI** y proporciona endpoints para gestionar todos los recursos de la aplicación de ligas de fútbol amateur.

La API sigue el prefijo base `/api/v1/` para todas las rutas y utiliza **JSON** como formato de intercambio de datos.

***

### 1. Información General

#### URL Base

```
http://localhost:8000/api/v1
```

#### Autenticación

La mayoría de endpoints requieren autenticación mediante **JWT (JSON Web Token)**.

Para endpoints protegidos, incluir el header:

```
Authorization: Bearer <token_jwt>
```

#### Documentación Interactiva

FastAPI genera documentación automática disponible en:

| Ruta | Descripción |
|------|-------------|
| `/docs` | Swagger UI - Documentación interactiva |
| `/redoc` | ReDoc - Documentación alternativa |
| `/openapi.json` | Especificación OpenAPI en formato JSON |

#### Endpoints de Salud

| Método | Ruta | Descripción |
|--------|------|-------------|
| GET | `/` | Información básica de la API |
| GET | `/health` | Estado de salud de la aplicación |

***

### 2. Autenticación (`/auth`)

Endpoints para la gestión de autenticación y tokens JWT.

| Método | Ruta | Descripción | Auth |
|--------|-----|-------------|------|
| POST | `/auth/login` | Iniciar sesión y obtener token JWT | No |
| GET | `/auth/me` | Obtener información del usuario autenticado | Sí |
| POST | `/auth/refresh` | Renovar token de acceso | No (refresh token) |

#### Ejemplo: Login

**Request:**

```http
POST /api/v1/auth/login
Content-Type: application/x-www-form-urlencoded

username=usuario@email.com&password=contrasena123
```

**Response:**

```json
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGci...",
    "token_type": "bearer"
}
```

#### Ejemplo: Obtener usuario actual

**Request:**

```http
GET /api/v1/auth/me
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGci...
```

**Response:**

```json
{
    "id_usuario": 1,
    "nombre": "Juan García",
    "email": "juan@email.com",
    "roles": [
        {"id_rol": 1, "nombre": "admin"}
    ]
}
```

***

### 3. Usuarios (`/usuarios`)

Gestión de cuentas de usuario del sistema.

| Método | Ruta | Descripción | Auth | Roles |
|--------|-----|-------------|------|-------|
| POST | `/usuarios/` | Registrar nuevo usuario | No | Público |
| GET | `/usuarios/` | Listar todos los usuarios | Sí | Admin |
| GET | `/usuarios/{id}` | Obtener usuario por ID | No | Público |
| PUT | `/usuarios/{id}` | Actualizar usuario | Sí | Propio/Admin |
| DELETE | `/usuarios/{id}` | Eliminar usuario | Sí | Admin |

#### Esquema UsuarioCreate

```json
{
    "nombre": "Juan García",
    "email": "juan@email.com",
    "contrasena": "contrasena123"
}
```

#### Esquema UsuarioResponse

```json
{
    "id_usuario": 1,
    "nombre": "Juan García",
    "email": "juan@email.com",
    "roles": []
}
```

***

### 4. Roles (`/roles`)

Gestión de roles y permisos del sistema.

| Método | Ruta | Descripción | Auth | Roles |
|--------|-----|-------------|------|-------|
| POST | `/roles/` | Crear nuevo rol | Sí | Admin |
| GET | `/roles/` | Listar todos los roles | No | Público |
| PUT | `/roles/{id}` | Actualizar rol | Sí | Admin |
| DELETE | `/roles/{id}` | Eliminar rol | Sí | Admin |
| POST | `/roles/asignar/{usuario_id}/{rol_id}` | Asignar rol a usuario | Sí | Admin |

#### Esquema RolCreate

```json
{
    "nombre": "coach",
    "descripcion": "Entrenador de equipo"
}
```

***

### 5. Ligas (`/ligas`)

Gestión de ligas y competiciones.

| Método | Ruta | Descripción | Auth | Roles |
|--------|-----|-------------|------|-------|
| POST | `/ligas/` | Crear nueva liga | Sí | Admin |
| GET | `/ligas/` | Listar todas las ligas | No | Público |
| GET | `/ligas/{id}` | Obtener liga por ID | No | Público |
| PUT | `/ligas/{id}` | Actualizar liga | Sí | Admin |
| DELETE | `/ligas/{id}` | Eliminar liga | Sí | Admin |

#### Esquema LigaCreate

```json
{
    "nombre": "Liga Municipal Primera",
    "pais": "España",
    "temporada": "2024-2025"
}
```

***

### 6. Equipos (`/equipos`)

Gestión de equipos de fútbol.

| Método | Ruta | Descripción | Auth | Roles |
|--------|-----|-------------|------|-------|
| POST | `/equipos/` | Crear nuevo equipo | Sí | Admin |
| GET | `/equipos/` | Listar todos los equipos | No | Público |
| GET | `/equipos/{id}` | Obtener equipo por ID | No | Público |
| PUT | `/equipos/{id}` | Actualizar equipo | Sí | Admin |
| DELETE | `/equipos/{id}` | Eliminar equipo | Sí | Admin |

#### Esquema EquipoCreate

```json
{
    "nombre": "Club Deportivo Ejemplo",
    "escudo_url": "https://...",
    "ciudad": "Madrid",
    "id_liga": 1
}
```

***

### 7. Jugadores (`/jugadores`)

Gestión de jugadores de fútbol.

| Método | Ruta | Descripción | Auth | Roles |
|--------|-----|-------------|------|-------|
| POST | `/jugadores/` | Crear nuevo jugador | Sí | Admin |
| GET | `/jugadores/` | Listar todos los jugadores | No | Público |
| GET | `/jugadores/{id}` | Obtener jugador por ID | No | Público |
| PUT | `/jugadores/{id}` | Actualizar jugador | Sí | Admin |
| DELETE | `/jugadores/{id}` | Eliminar jugador | Sí | Admin |

#### Esquema JugadorCreate

```json
{
    "id_usuario": 1,
    "id_equipo": 2,
    "posicion": "Delantero",
    "dorsal": 9,
    "altura": 1.80,
    "peso": 75.5,
    "pie_dominante": "derecho"
}
```

***

### 8. Partidos (`/partidos`)

Gestión de partidos de fútbol.

| Método | Ruta | Descripción | Auth | Roles |
|--------|-----|-------------|------|-------|
| POST | `/partidos/` | Crear nuevo partido | Sí | Admin |
| GET | `/partidos/` | Listar todos los partidos | No | Público |
| GET | `/partidos/{id}` | Obtener partido por ID | No | Público |
| PUT | `/partidos/{id}` | Actualizar partido | Sí | Admin |
| DELETE | `/partidos/{id}` | Eliminar partido | Sí | Admin |

#### Esquema PartidoCreate

```json
{
    "id_equipo_local": 1,
    "id_equipo_visitante": 2,
    "id_liga": 1,
    "fecha": "2024-03-15T18:00:00",
    "estadio": "Estadio Municipal",
    "goles_local": 0,
    "goles_visitante": 0
}
```

***

### 9. Eventos (`/eventos`)

Gestión de eventos durante los partidos (goles, tarjetas, sustituciones).

| Método | Ruta | Descripción | Auth | Roles |
|--------|-----|-------------|------|-------|
| POST | `/eventos/` | Registrar evento en partido | Sí | Delegado |
| GET | `/eventos/partido/{partido_id}` | Listar eventos de un partido | No | Público |

#### Esquema EventoPartidoCreate

```json
{
    "id_partido": 1,
    "id_jugador": 5,
    "minuto": 45,
    "tipo_evento": "gol",
    "descripcion": "Gol de cabeza tras centro"
}
```

#### Tipos de eventos

| Tipo | Descripción |
|------|-------------|
| `gol` | Gol marcado |
| `tarjeta_amarilla` | Tarjeta amarilla |
| `tarjeta_roja` | Tarjeta roja |
| `sustitucion_entrada` | Jugador que entra |
| `sustitucion_salida` | Jugador que sale |

***

### 10. Convocatorias (`/convocatorias`)

Gestión de la lista de jugadores llamados para un partido.

| Método | Ruta | Descripción | Auth | Roles |
|--------|-----|-------------|------|-------|
| POST | `/convocatorias/` | Crear convocatoria | Sí | Admin/Coach |
| GET | `/convocatorias/partido/{id}` | Listar jugadores convocados | Sí | Usuario |

***

### 11. Alineaciones (`/alineaciones`)

Gestión de los jugadores que inician el encuentro y sus posiciones.

| Método | Ruta | Descripción | Auth | Roles |
|--------|-----|-------------|------|-------|
| POST | `/alineaciones/` | Definir alineación inicial | Sí | Admin/Coach |
| GET | `/alineaciones/partido/{id}` | Consultar alineación de un partido | No | Público |

***

### 12. Imágenes (`/imagenes`)

Gestión de subida y almacenamiento de archivos integrados con Supabase Storage.

| Método | Ruta | Descripción | Auth | Roles |
|--------|-----|-------------|------|-------|
| POST | `/imagenes/upload` | Subir imagen (escudo/logo) | Sí | Admin |
| GET | `/imagenes/{id}` | Obtener URL de imagen | No | Público |

***

### 13. Estadísticas (`/estadisticas`)

Cálculo de métricas de rendimiento para ligas, equipos y jugadores.

| Método | Ruta | Descripción | Auth | Roles |
|--------|-----|-------------|------|-------|
| GET | `/estadisticas/liga/{id}` | Clasificación general de la liga | No | Público |
| GET | `/estadisticas/jugador/{id}` | Rendimiento individual del jugador | No | Público |

***

### 14. Público (`/public`)

Endpoints accesibles sin autenticación para visualización externa.

| Método | Ruta | Descripción | Auth | Roles |
|--------|-----|-------------|------|-------|
| GET | `/public/ligas` | Listado público de todas las ligas | No | Público |
| GET | `/public/partidos/en-vivo` | Partidos que se están jugando actualmente | No | Público |

***

### 15. Configuración de Liga (`/liga_configuracion`)

Ajustes específicos de la competición y reglas internas.

| Método | Ruta | Descripción | Auth | Roles |
|--------|-----|-------------|------|-------|
| GET | `/liga_configuracion/{id}` | Obtener parámetros de la liga | Sí | Admin |
| PUT | `/liga_configuracion/{id}` | Actualizar configuración de la liga | Sí | Admin |

***

### 16. Tokens de Recuperación (`/tokens_recuperacion`)

Gestión del flujo de seguridad para el restablecimiento de contraseñas.

| Método | Ruta | Descripción | Auth | Roles |
|--------|-----|-------------|------|-------|
| POST | `/tokens_recuperacion/solicitar` | Generar token de reset vía email | No | Público |
| POST | `/tokens_recuperacion/validar` | Verificar token antes de cambiar password | No | Público |

***

### 17. Notificaciones (`/notificaciones`)

Gestión de notificaciones push y alertas de usuario.

| Método | Ruta | Descripción | Auth | Roles |
|--------|-----|-------------|------|-------|
| GET | `/notificaciones/` | Listar notificaciones del usuario | Sí | Usuario |
| PUT | `/notificaciones/{id}` | Marcar notificación como leída | Sí | Usuario |

***

### 18. Códigos de Respuesta HTTP

La API utiliza códigos HTTP estándar:

| Código | Descripción |
|--------|-------------|
| `200` | OK - Petición exitosa |
| `201` | Created - Recurso creado correctamente |
| `400` | Bad Request - Datos de entrada inválidos |
| `401` | Unauthorized - Token JWT inválido o expirado |
| `403` | Forbidden - Sin permisos para realizar la acción |
| `404` | Not Found - Recurso no encontrado |
| `422` | Unprocessable Entity - Error de validación |
| `500` | Internal Server Error - Error del servidor |

***

### 19. Ejemplos de Uso

#### Obtener token de autenticación

```bash
curl -X POST "http://localhost:8000/api/v1/auth/login" \
     -H "Content-Type: application/x-www-form-urlencoded" \
     -d "username=usuario@email.com&password=contrasena123"
```

#### Crear un equipo (requiere admin)

```bash
curl -X POST "http://localhost:8000/api/v1/equipos/" \
     -H "Authorization: Bearer <token>" \
     -H "Content-Type: application/json" \
     -d '{"nombre":"Equipo Test","ciudad":"Madrid"}'
```

#### Listar todos los equipos (público)

```bash
curl -X GET "http://localhost:8000/api/v1/equipos/"
```

#### Obtener usuario autenticado

```bash
curl -X GET "http://localhost:8000/api/v1/auth/me" \
     -H "Authorization: Bearer <token>"
```
