# Autenticación JWT

El sistema de autenticación del backend está basado en **JSON Web Tokens (JWT)**, un estándar abierto (RFC 7519) que permite transmitir información entre partes de forma segura como un objeto JSON.

Este sistema permite que los usuarios se autentiquen una vez y reciban un token que pueden usar para acceder a recursos protegidos sin necesidad de enviar credenciales en cada petición.

***

### 1. Conceptos Básicos

#### ¿Qué es JWT?

Un JWT es un token codificado que contiene tres partes separadas por puntos:

```
xxxxx.yyyyy.zzzzz
```

| Parte | Descripción |
|-------|-------------|
| Header | Algoritmo de firma (HS256) y tipo de token |
| Payload | Datos del usuario (ID, expiración) |
| Signature | Firma criptográfica para verificar autenticidad |

#### Flujo de Autenticación

```
1. Cliente envía credenciales (email + password)
   POST /auth/login

2. Servidor valida credenciales en base de datos

3. Servidor genera JWT con ID de usuario
   └── Token firmado con SECRET_KEY

4. Servidor devuelve token al cliente
   {"access_token": "...", "token_type": "bearer"}

5. Cliente almacena token (localStorage/sessionStorage)

6. En cada petición protegida:
   └── Header: Authorization: Bearer <token>

7. Servidor valida token y extrae usuario
   └── Si es válido, procesa la petición
   └── Si no, devuelve 401 Unauthorized
```

***

### 2. Configuración JWT

La configuración de JWT se encuentra en `app/config.py` y utiliza variables de entorno:

```python
SECRET_KEY = settings.SECRET_KEY          # Clave secreta para firmar tokens
ALGORITHM = settings.ALGORITHM            # Algoritmo de firma (HS256)
ACCESS_TOKEN_EXPIRE_MINUTES = settings.ACCESS_TOKEN_EXPIRE_MINUTES  # Tiempo de expiración
```

#### Variables de entorno (.env)

```env
SECRET_KEY=tu_clave_secreta_aqui_cambiar
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=60
```

#### Generar SECRET_KEY segura

```bash
python -c "import secrets; print(secrets.token_urlsafe(64))"
```

***

### 3. Generación de Tokens

La función `create_access_token` en `app/api/dependencies.py` genera los tokens JWT:

```python
from jose import jwt
from datetime import datetime, timedelta

def create_access_token(data: dict, expires_delta: timedelta | None = None):
    to_encode = data.copy()

    if expires_delta:
        expire = datetime.utcnow() + expires_delta
    else:
        expire = datetime.utcnow() + timedelta(minutes=ACCESS_TOKEN_EXPIRE_MINUTES)

    to_encode.update({"exp": expire})

    encoded_jwt = jwt.encode(to_encode, SECRET_KEY, algorithm=ALGORITHM)
    return encoded_jwt
```

#### Payload del Token

El payload contiene:

```json
{
    "sub": "1",           // ID del usuario (subject)
    "exp": 1710456789     // Timestamp de expiración
}
```

| Campo | Descripción |
|-------|-------------|
| `sub` | Identificador único del usuario (ID) |
| `exp` | Fecha y hora de expiración del token |

***

### 4. Endpoint de Login

El endpoint `/auth/login` procesa las credenciales y devuelve el token:

**Ruta:** `POST /api/v1/auth/login`

**Request:**

```http
POST /api/v1/auth/login
Content-Type: application/x-www-form-urlencoded

username=usuario@email.com&password=contrasena123
```

> **Nota:** Se utiliza `OAuth2PasswordRequestForm` de FastAPI, que espera campos `username` y `password`.

**Response (éxito):**

```json
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...",
    "token_type": "bearer"
}
```

**Response (error):**

```json
{
    "detail": "Credenciales incorrectas"
}
```

**Código del endpoint:**

```python
@router.post("/login")
def login(
    form_data: OAuth2PasswordRequestForm = Depends(),
    db: Session = Depends(get_db)
):
    # Autenticar usuario
    usuario = autenticar_usuario(db, form_data.username, form_data.password)

    if not usuario:
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Credenciales incorrectas"
        )

    # Crear token
    access_token_expires = timedelta(minutes=ACCESS_TOKEN_EXPIRE_MINUTES)
    access_token = create_access_token(
        data={"sub": str(usuario.id_usuario)},
        expires_delta=access_token_expires
    )

    return {"access_token": access_token, "token_type": "bearer"}
```

***

### 5. Validación de Tokens

La función `get_current_user` valida el token y obtiene el usuario:

```python
from fastapi import Depends, HTTPException, status
from fastapi.security import OAuth2PasswordBearer
from jose import jwt, JWTError

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="/auth/login")

def get_current_user(
    token: str = Depends(oauth2_scheme),
    db=Depends(get_db)
):
    credenciales_invalidas = HTTPException(
        status_code=status.HTTP_401_UNAUTHORIZED,
        detail="Token inválido o expirado",
        headers={"WWW-Authenticate": "Bearer"},
    )

    try:
        # Decodificar token
        payload = jwt.decode(token, SECRET_KEY, algorithms=[ALGORITHM])
        user_id_str = payload.get("sub")

        if user_id_str is None:
            raise credenciales_invalidas

        user_id = int(user_id_str)

    except (JWTError, ValueError):
        raise credenciales_invalidas

    # Buscar usuario en BD
    usuario = obtener_usuario_por_id(db, user_id)

    if usuario is None:
        raise credenciales_invalidas

    return usuario
```

***

### 6. Protección de Endpoints

#### Endpoint protegido con autenticación

```python
@router.get("/me", response_model=UsuarioResponse)
def obtener_usuario_actual(current_user = Depends(get_current_user)):
    return current_user
```

#### Endpoint protegido con rol específico

```python
@router.post("/", dependencies=[Depends(require_role("admin"))])
def crear_usuario(usuario: UsuarioCreate, db: Session = Depends(get_db)):
    return crear_usuario(db, usuario)
```

#### Función require_role

```python
def require_role(role_name: str):
    def role_checker(current_user = Depends(get_current_user)):
        roles = [rol.nombre for rol in current_user.roles]

        if role_name not in roles:
            raise HTTPException(
                status_code=status.HTTP_403_FORBIDDEN,
                detail=f"No tienes permisos (se requiere rol '{role_name}')"
            )
        return True

    return role_checker
```

***

### 7. Sistema de Roles

El sistema implementa control de acceso basado en roles (RBAC):

| Rol | Permisos |
|-----|----------|
| `admin` | Acceso total a todas las funcionalidades |
| `coach` | Gestión de su equipo y formaciones |
| `delegate` | Registrar eventos de partidos |
| `player` | Ver su propia información |
| `viewer` | Ver información pública |

#### Estructura de la relación Usuario-Rol

```
usuarios (tabla)
    │
    ├── usuario_rol (tabla intermedia)
    │
    └── roles (tabla)
```

Un usuario puede tener múltiples roles asignados.

***

### 8. Refresh Token

El endpoint `/auth/refresh` permite renovar el token de acceso sin volver a iniciar sesión:

**Ruta:** `POST /api/v1/auth/refresh`

**Request:**

```json
{
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9..."
}
```

**Response:**

```json
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...",
    "token_type": "bearer"
}
```

**Código del endpoint:**

```python
@router.post("/refresh")
def refresh_token(token: str, db: Session = Depends(get_db)):
    try:
        payload = jwt.decode(token, SECRET_KEY, algorithms=[ALGORITHM])
        user_id = payload.get("sub")

        if user_id is None:
            raise HTTPException(401, "Refresh token inválido")

    except JWTError:
        raise HTTPException(401, "Refresh token inválido")

    usuario = obtener_usuario_por_id(db, user_id)

    if not usuario:
        raise HTTPException(401, "Refresh token inválido")

    nuevo_access_token = create_access_token({"sub": str(usuario.id_usuario)})

    return {"access_token": nuevo_access_token, "token_type": "bearer"}
```

***

### 9. Uso desde el Cliente

#### Cabeceras HTTP

Para cada petición a endpoints protegidos:

```http
GET /api/v1/auth/me
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...
```

#### Ejemplo con Fetch (JavaScript)

```javascript
// Login
const loginResponse = await fetch('http://localhost:8000/api/v1/auth/login', {
    method: 'POST',
    headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
    body: 'username=user@email.com&password=password123'
});

const { access_token } = await loginResponse.json();

// Guardar token
localStorage.setItem('token', access_token);

// Petición autenticada
const userResponse = await fetch('http://localhost:8000/api/v1/auth/me', {
    headers: { 'Authorization': `Bearer ${localStorage.getItem('token')}` }
});

const user = await userResponse.json();
```

#### Ejemplo con Axios (JavaScript)

```javascript
import axios from 'axios';

// Configurar interceptor para añadir token automáticamente
axios.interceptors.request.use(config => {
    const token = localStorage.getItem('token');
    if (token) {
        config.headers.Authorization = `Bearer ${token}`;
    }
    return config;
});

// Login
const { data } = await axios.post('/api/v1/auth/login',
    new URLSearchParams({ username: 'user@email.com', password: 'password123' })
);

localStorage.setItem('token', data.access_token);

// Petición autenticada (token se añade automáticamente)
const { data: user } = await axios.get('/api/v1/auth/me');
```

***

### 10. Consideraciones de Seguridad

#### Buenas Prácticas Implementadas

| Práctica | Descripción |
|----------|-------------|
| Clave secreta segura | Usar `secrets.token_urlsafe(64)` para generar SECRET_KEY |
| Expiración de token | Tokens con tiempo de vida limitado (60 minutos por defecto) |
| HTTPS en producción | Tokens viajan en headers, deben ir cifrados |
| No almacenar datos sensibles | El token solo contiene el ID del usuario |

#### Recomendaciones para Producción

1. **Usar HTTPS obligatoriamente** - Los tokens pueden ser interceptados en HTTP
2. **Rotar la SECRET_KEY periódicamente** - Invalida todos los tokens anteriores
3. **Implementar lista negra de tokens** - Para revocación de sesiones
4. **Reducir tiempo de expiración** - 15-30 minutos para aplicaciones sensibles
5. **Implementar rate limiting** - Prevenir ataques de fuerza bruta en `/auth/login`

***

### 11. Flujo Completo de Autenticación

```
┌─────────────┐                    ┌─────────────┐                 ┌────────────┐
│   Cliente   │                    │   Backend   │                 │   Base de  │
│   (Front)   │                    │  (FastAPI)  │                 │    Datos   │
└──────┬──────┘                    └──────┬──────┘                 └──────┬─────┘
       │                                  │                               │
       │  POST /auth/login                │                               │
       │  (email + password)              │                               │
       │ ────────────────────────────────>│                               │
       │                                  │  Buscar usuario               │
       │                                  │ ─────────────────────────────>│
       │                                  │                               │
       │                                  │  Datos del usuario            │
       │                                  │ <──────────────────────────── │
       │                                  │                               │
       │                                  │  Verificar contraseña         │
       │                                  │  (bcrypt verify)              │
       │                                  │                               │
       │                                  │  Generar JWT                  │
       │                                  │  jwt.encode({sub: user_id})   │
       │                                  │                               │
       │  access_token                    │                               │
       │ <─────────────────────────────── │                               │
       │                                  │                               │
       │  GET /auth/me                    │                               │
       │  Authorization: Bearer <token>   │                               │
       │ ────────────────────────────────>│                               │
       │                                  │  Validar JWT                  │
       │                                  │  jwt.decode(token)            │
       │                                  │                               │
       │                                  │  Obtener user_id del token    │
       │                                  │                               │
       │                                  │  Buscar usuario por ID        │
       │                                  │ ─────────────────────────────>│
       │                                  │                               │
       │                                  │  Datos del usuario            │
       │                                  │ <──────────────────────────── │
       │                                  │                               │
       │  Datos del usuario autenticado   │                               │
       │ <─────────────────────────────── │                               │
	   │                                  │                               │
       └─────────────────────────────────┘└──────────────────────────────┘
```