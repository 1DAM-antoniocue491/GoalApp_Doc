# Despliegue del Frontend Web

El frontend web de GoalApp está optimizado para un despliegue continuo y escalable utilizando la infraestructura de **Firebase Hosting**.

## 1. Plataforma de Hosting
Se ha seleccionado Firebase Hosting por su capacidad de servir contenido estático a través de una CDN global, garantizando tiempos de carga mínimos y una integración nativa con el ecosistema de Google.

## 2. Flujo de Despliegue y Ejecución

El proceso de despliegue sigue un flujo automatizado para asegurar que solo código validado llegue a producción. A continuación, se detalla el procedimiento paso a paso para ejecutarlo desde un entorno local:

### Paso 1: Preparación del Entorno
Asegúrese de tener instaladas las herramientas de Firebase y de haber iniciado sesión:
```bash
npm install -g firebase-tools
firebase login
```

### Paso 2: Configuración del Proyecto
Vincule el repositorio local con el proyecto de Firebase:
```bash
firebase init hosting
```
*Durante la configuración, seleccione el proyecto GoalApp y defina la carpeta `dist` como el directorio público.*

### Paso 3: Configuración de Variables de Producción
Cree o edite el archivo `.env.production` en la raíz del proyecto para apuntar al backend de Render:
```env
VITE_API_URL=https://goalapp-api.onrender.com
```

### Paso 4: Generación del Build Optimizado
Ejecute el comando de Vite para compilar la aplicación en modo producción:
```bash
npm run build
```
*Este paso optimiza los activos, minifica el JS y genera el bundle final en la carpeta `dist/`.*

### Paso 5: Ejecución del Despliegue
Suba los archivos compilados a la infraestructura de Firebase:
```bash
firebase deploy --only hosting
```

---

## 3. Configuración Técnica
La configuración del despliegue se define en el archivo `firebase.json` en la raíz del proyecto:
- **Public Directory**: Se define la carpeta `dist` como el origen de los archivos públicos.
- **Rewrites**: Para soportar el routing del lado del cliente (React Router), se ha configurado una regla de reescritura que redirige todas las peticiones que no coincidan con un archivo físico hacia `index.html`.

## 4. Gestión de Variables de Entorno
Las URLs de la API y otras claves sensibles se gestionan mediante archivos `.env.production`. 
- Durante el proceso de build, Vite inyecta estas variables en el código final.
- La URL del backend (desplegado en Render) se configura como la variable `VITE_API_URL`.

## 5. Estrategia de Versiones
Firebase Hosting permite mantener un historial de despliegues, facilitando la reversión inmediata (**rollback**) a una versión anterior en caso de detectar errores críticos en producción.
