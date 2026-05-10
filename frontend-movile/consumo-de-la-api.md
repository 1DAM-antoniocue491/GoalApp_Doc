# Consumo de la API en Frontend Móvil

La capa de red del frontend móvil está diseñada para ser extremadamente resiliente, anticipando los problemas de conectividad comunes en dispositivos móviles.

### 1. Cliente HTTP y Configuración

El cliente de API, ubicado en `shared/api/client.ts`, es una implementación personalizada basada en la API nativa de `fetch`.

**Características principales:**
- **Timeouts**: Implementación de `AbortController` con un tiempo de espera configurable (`ENV.REQUEST_TIMEOUT`) para evitar que la app se quede congelada esperando una respuesta.
- **Inyección de Tokens**: Interceptores que añaden automáticamente la cabecera `Authorization: Bearer <token>` recuperada del almacenamiento seguro.

### 2. Resiliencia: Backoff Exponencial

Para mejorar la experiencia del usuario en condiciones de red inestables, la aplicación implementa un sistema de **reintentos con retroceso exponencial**:

Cuando ocurre un error de red o un error de servidor (`5xx`), el cliente no falla inmediatamente, sino que reintenta la petición siguiendo esta fórmula de tiempo:
`Tiempo de espera = 2 ^ (número de reintentos) * 1000ms`

- **Reintento 1**: 1 segundo.
- **Reintento 2**: 2 segundos.
- **Reintento 3**: 4 segundos.
- ...hasta alcanzar el límite definido en `ENV.MAX_RETRIES`.

### 3. Manejo de Errores

El sistema de red clasifica los errores para proporcionar el feedback adecuado:
- **401 Unauthorized**: Dispara el flujo de `refresh_token`.
- **403 Forbidden**: Informa al usuario que no tiene permisos para esa acción.
- **422 Unprocessable Entity**: Mapea los errores de validación del backend para mostrarlos en los formularios.
- **Errores de Red**: Activa el mecanismo de reintentos antes de mostrar un mensaje de "Sin conexión".

### 4. Flujo de Datos

La aplicación separa la petición de la gestión del estado:
`UI Component` $\rightarrow$ `Custom Hook` $\rightarrow$ `Feature Service` $\rightarrow$ `API Client` $\rightarrow$ `Backend`
