# Consumo de la API en Frontend Web

El frontend de GoalApp utiliza una arquitectura de red centralizada y resiliente para comunicarse con el backend de FastAPI.

### 1. Cliente de API (`apiClient`)

La comunicación se realiza a través de una instancia configurada de **Axios**, ubicada en `src/services/api/client.ts`.

**Configuraciones clave:**
- **BaseURL**: Configurada dinámicamente desde variables de entorno para soportar desarrollo y producción.
- **Timeouts**: Tiempo de espera configurado para evitar peticiones colgadas.
- **Headers**: Inyección automática del token `Bearer` en cada petición autenticada.

### 2. Interceptores de Request

El cliente de API cuenta con un interceptor que añade automáticamente el token de acceso desde `localStorage` a la cabecera `Authorization` de cada petición:

```typescript
config.headers.Authorization = `Bearer ${token}`;
```

### 3. Interceptores de Response y Manejo de Errores

El sistema implementa una gestión de errores robusta mediante interceptores de respuesta:

#### A. Manejo de Errores 401 (Refresh Token Queue)
Cuando la API devuelve un `401 Unauthorized`, el sistema no redirige inmediatamente al login, sino que:
1. **Pausa**: Añade la petición fallida a una cola de espera (`failedQueue`).
2. **Renueva**: Llama al endpoint `/auth/refresh` para obtener un nuevo token.
3. **Reintenta**: Una vez obtenido el nuevo token, procesa todas las peticiones de la cola con el token actualizado.

#### B. Otros Códigos de Error
- **403 Forbidden**: Captura errores de permisos insuficientes y lanza un `ApiError` con el mensaje del servidor.
- **422 Unprocessable Entity**: Transforma los errores de validación de Pydantic (arrays de errores) en mensajes de texto legibles para el usuario.
- **500+ / Network Error**: Implementa una lógica de reintento automático (`API_RETRY_COUNT`) antes de mostrar un error final.

### 4. Patrón de Consumo en Features

Para mantener la separación de responsabilidades, cada feature tiene su propio archivo de servicios:

`src/features/[nombre-feature]/services/api.ts`

**Ejemplo de flujo:**
`Componente` $\rightarrow$ `Hook de Feature` $\rightarrow$ `Servicio de Feature` $\rightarrow$ `apiClient (Axios)` $\rightarrow$ `Backend`
