# Dificultades Encontradas en el Proyecto GoalApp

Durante el desarrollo de GoalApp, se han identificado y superado diversas dificultades técnicas y organizativas que han marcado la evolución del sistema.

### 1. Sincronización de Documentación y Código
La brecha más significativa fue el desfase entre la implementación real y la documentación técnica. El código avanzó rápidamente hacia una arquitectura profesional, mientras que los documentos permanecieron en estados iniciales o basados en tecnologías obsoletas.
- **Solución**: Se realizó una auditoría completa de los tres repositorios (Backend, Web y Móvil) para reconstruir la documentación basándose en la implementación real.

### 2. Resiliencia de Red en Dispositivos Móviles
La naturaleza inestable de las conexiones móviles generaba fallos críticos en la experiencia de usuario.
- **Dificultad**: Peticiones que se quedaban colgadas o fallaban sin feedback claro.
- **Solución**: Implementación de un cliente HTTP personalizado con `AbortController` para timeouts y la adopción de un algoritmo de **Backoff Exponencial** para reintentos automáticos en errores 5xx y fallos de red.

### 3. Complejidad del Sistema de Permisos
El sistema de roles (`admin`, `coach`, `delegate`, `player`, `viewer`) requería un control muy granular para evitar que un usuario accediera a funciones de otro rol.
- **Dificultad**: Gestionar la jerarquía de permisos y asegurar que la UI se adaptara dinámicamente al rol del usuario en tiempo real.
- **Solución**: Implementación de un sistema de roles basado en base de datos con tablas intermedias y validaciones estrictas en el backend mediante dependencias de FastAPI.

### 4. Evolución del Modelo de Datos
El sistema sufrió cambios estructurales importantes a medida que se comprendían mejor las necesidades del fútbol.
- **Cambio Crítico**: La eliminación total del sistema complejo de formaciones tácticas y posiciones fijas en favor de un sistema de alineaciones basado en strings, proporcionando la flexibilidad necesaria para los entrenadores.
- **Migración**: El cambio de MySQL a PostgreSQL (vía Supabase) para aprovechar la integridad referencial y el rendimiento en consultas estadísticas.

### 5. Gestión de Concurrencia en la Autenticación
El manejo de tokens JWT y la actualización de los mismos (`refresh_token`) presentaba problemas cuando múltiples peticiones fallaban simultáneamente con un error 401.
- **Dificultad**: Evitar que la aplicación disparara múltiples peticiones de refresco al mismo tiempo, lo que invalidaba los tokens.
- **Solución**: Creación de una cola de suscriptores (`failedQueue` en Web y `refreshSubscribers` en Móvil) que pausa las peticiones pendientes hasta que el nuevo token es obtenido y validado.

### 6. Despliegue y CORS
La configuración del entorno de producción en Render presentó desafíos con la política de intercambio de recursos cruzados (CORS).
- **Dificultad**: Bloqueos de peticiones desde el frontend web hacia la API debido a la configuración de dominios.
- **Solución**: Ajuste preciso de los `CORSMiddleware` en FastAPI para permitir el tráfico solo desde los dominios autorizados de producción.
