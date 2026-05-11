# Despliegue

## Cómo generé las versiones Android de GoalApp

Este documento resume el proceso que seguí para generar las dos versiones Android de la aplicación **GoalApp**. La aplicación está desarrollada con **React Native**, **Expo**, **NativeWind** y **TailwindCSS**, y se ha compilado usando **EAS Build**, que es el sistema de compilación en la nube de Expo.

La idea era tener dos archivos distintos:

* un archivo **.aab**, pensado para subir la aplicación a Google Play Console;
* un archivo **.apk**, pensado para poder instalar la aplicación directamente en un móvil Android y probarla sin pasar por Play Store.

***

### 1. Por qué necesitaba dos archivos distintos

En Android no se utiliza siempre el mismo archivo para todo.

El archivo **.aab** es el que se utiliza normalmente para publicar una aplicación en Google Play. No se instala directamente en el móvil como si fuera una aplicación normal, sino que se sube a Google Play Console y desde ahí Google se encarga de generar las versiones necesarias para cada dispositivo.

El archivo **.apk**, en cambio, sí se puede instalar directamente en un móvil Android. Por eso es útil para enseñar el proyecto, probarlo en un dispositivo real o entregarlo como demo.

En resumen:

```txt

.aab  -> para Google Play

.apk  -> para instalar directamente en Android

```

***

### 2. Archivos importantes del proyecto

En la raíz del proyecto tenía estos archivos de configuración:

```txt

goal-app/
├─ app.json
├─ eas.json
├─ package.json
├─ package-lock.json
├─ global.css
├─ metro.config.js
├─ nativewind-env.d.ts
├─ postcss.config.mjs
├─ tsconfig.json
└─ .env

```

Los más importantes para generar las versiones fueron:

```txt

app.json
eas.json
package.json
package-lock.json
metro.config.js
global.css
postcss.config.mjs

```

El archivo `app.json` contiene la configuración principal de Expo, como el nombre de la aplicación, el identificador de Android y otros datos generales.

El archivo `eas.json` es el que define cómo se deben generar las versiones con EAS.

***

### 3. Configuración de EAS

Para poder generar los dos tipos de archivo, el archivo `eas.json` debe tener dos perfiles principales: uno para producción y otro para generar un APK instalable.

Una configuración válida es esta:

```json

{

“cli": {
    “version": “>= 13.0.0",
    “appVersionSource": “remote"
},
“build": {
    “preview": {
        “distribution": “internal",
            “android": {
                “buildType": “apk"
            }
        },
        “production": {
            “autoIncrement": true,
                “android": {
                    “buildType": “app-bundle"
                }
            }
        }
}

```

El perfil `production` genera el archivo `.aab`.

El perfil `preview` genera el archivo `.apk`.

***

### 4. Pasos iniciales que seguí antes de lanzar las versiones

Antes de llegar a generar los archivos finales, preparé el proyecto desde la raíz de la carpeta de la aplicación. En mi caso, la carpeta del proyecto era `goal-app`, y desde ahí se ejecutaron los comandos.

Primero instalé la herramienta de EAS, que es la que permite generar las versiones desde Expo:

```powershell

npm install -g eas-cli

```

Después inicié sesión con la cuenta de Expo:

```powershell

eas login

```

También revisé las dependencias relacionadas con NativeWind y TailwindCSS. La guía base que seguí indicaba instalar o comprobar estas dependencias:

```powershell

npm install nativewind react-native-reanimated react-native-safe-area-context

npm install --save-dev tailwindcss@^3.4.17 prettier-plugin-tailwindcss@^0.5.11 babel-preset-expo

```

En mi caso, esta parte necesitó revisión porque el proyecto tenía una configuración más moderna de NativeWind. Por eso hubo que comprobar bien las versiones instaladas y ajustar las dependencias para que no hubiese conflicto entre NativeWind y TailwindCSS.

También revisé que la configuración de NativeWind estuviera preparada, porque si esto falla la aplicación puede compilar, pero luego los estilos no se ven bien. Los puntos que comprobé fueron:

```txt

metro.config.js
postcss.config.mjs
global.css
nativewind-env.d.ts

```

Además, la aplicación tenía que importar el archivo `global.css`, porque ahí es donde se cargan los estilos de Tailwind/NativeWind.

Después configuré EAS en el proyecto:

```powershell

eas build:configure

```

Este comando generó o actualizó el archivo `eas.json`. También vinculó el proyecto local con el proyecto de Expo cuando EAS detectó que ya existía un proyecto asociado.

En la terminal apareció algo parecido a esto:

```txt

Generated eas.json.
Existing EAS project found for @kevinho_05/goal-app.
Linked local project to EAS project.

```

A partir de ahí ya se podían lanzar las versiones de Android.

***

### 5. Comprobaciones antes de compilar

Antes de lanzar la versión hice varias comprobaciones para evitar errores.

Primero comprobé que Expo pudiera leer bien la configuración del proyecto:

```powershell

npx expo config --json

```

Después revisé TypeScript:

```powershell

npx tsc --noEmit

```

Y también pasé la revisión de Expo:

```powershell

npx expo-doctor

```

Estas comprobaciones no generan la aplicación, pero ayudan a detectar problemas antes de subir el proyecto a EAS.

***

### 6. Problemas que aparecieron durante el proceso

Durante el proceso no salió todo a la primera. Hubo varios errores de dependencias que hubo que corregir.

#### Error con `expo-asset`

Uno de los errores indicaba que faltaba una dependencia llamada `pngjs`:

```txt

Cannot find module 'node_modules/pngjs/lib/png.js'

```

Lo solucioné instalando la dependencia y actualizando `expo-asset`:

```powershell

npm install pngjs
npx expo install expo-asset

```

#### Error con `isexe`

También apareció un error indicando que faltaba un archivo dentro de `node_modules`:

```txt

Cannot find module 'node_modules/isexe/index.js'

```

Ese error indicaba que la instalación de dependencias estaba dañada o incompleta. Para solucionarlo limpié la instalación y volví a instalar todo:

```powershell

Remove-Item -Recurse -Force node_modules
Remove-Item -Force package-lock.json
npm cache clean --force
npm install

```

#### Conflicto entre NativeWind y TailwindCSS

También hubo un conflicto de versiones. El proyecto estaba usando **NativeWind v5 preview**, que necesita una versión moderna de TailwindCSS.

El error indicaba algo parecido a esto:

```txt

nativewind necesita tailwindcss > 4.1.11

```

La solución fue instalar versiones compatibles:

```powershell

npm install nativewind@preview react-native-css react-native-reanimated react-native-safe-area-context

npm install --save-dev tailwindcss@latest @tailwindcss/postcss

```

Después de esto, el proyecto pudo volver a instalar correctamente sus dependencias.

***

### 7. Generación del archivo .aab para Google Play

Para generar la versión de producción ejecuté este comando:

```powershell

eas build --platform android --profile production

```

Es importante poner `--platform android`, porque si no se indica la plataforma EAS puede intentar preparar también una versión de iOS y pedir credenciales de Apple.

Durante el proceso EAS hizo varias cosas:

* vinculó el proyecto local con el proyecto de Expo;
* usó las credenciales remotas de Android;
* incrementó el `versionCode`;
* comprimió el proyecto;
* subió los archivos a EAS;
* empezó la compilación en la nube.

En la página de EAS la versión aparecía como:

```txt

Android Play Store build
Profile: production
Environment: production
SDK version: 54.0.0
Version: 1.0.0 (4)
Status: Build in progress

```

Cuando esta versión termina correctamente, el resultado es un archivo `.aab`.

Este archivo es el que se puede subir a Google Play Console.

***

### 8. Qué hacer con el archivo .aab

El archivo `.aab` no se instala directamente en el móvil. Su uso principal es subirlo a **Google Play Console**.

Los pasos generales serían:

1. Entrar en Google Play Console.
2. Crear la aplicación.
3. Completar la ficha de la aplicación.
4. Añadir icono, capturas y descripción.
5. Configurar la clasificación de contenido.
6. Revisar las políticas de privacidad y datos.
7. Entrar en una pista de publicación, por ejemplo prueba interna.
8. Subir el archivo `.aab`.
9. Revisar las advertencias de Google Play.
10. Enviar la versión a revisión.

Para un proyecto de fin de curso, no siempre es necesario publicar la aplicación oficialmente. Puede bastar con enseñar que existe una versión `.aab` preparada para Google Play.

***

### 9. Generación del archivo .apk para instalar en un móvil

Además del `.aab`, también necesitaba un archivo instalable directamente en un dispositivo Android.

Para eso se utiliza el perfil `preview`:

```powershell

eas build --platform android --profile preview

```

Para configurar el perfil en `eas.json`, debes agregar lo siguiente:

```json

"preview": {
    “distribution": “internal",
    “android": {
        “buildType": “apk"
    }
}

```

Cuando EAS termine de construir la aplicación, obtendrás un archivo `.apk`. Este archivo se puede instalar directamente en un dispositivo Android.

En mi caso, la aplicación instalable se asoció con este enlace de Expo:

```txt

https://expo.dev/accounts/kevinho_05/projects/goal-app/builds/f8b095fb-2dad-4229-9576-e7628f40648b

```

Después de que EAS finalizó la construcción, apareció un mensaje en la terminal indicando que la aplicación se había construido correctamente. También se mostró un código QR y un enlace para abrir la aplicación desde un dispositivo Android.

En la página de Expo, había una ventana de instalación llamada **Instalar en un dispositivo de prueba**. Desde allí, podía instalar la aplicación de Android escaneando el código QR con la cámara del dispositivo o abriendo el enlace directamente desde el dispositivo.

En las capturas que guardé, se veían dos cosas importantes:

```txt

1. La terminal indicando que la aplicación se había construido correctamente.
2. La ventana de Expo con el código QR para instalar la aplicación en un dispositivo de prueba.

```

Esto me permitió comprobar que la aplicación no solo estaba preparada para la tienda de aplicaciones, sino que también podía instalarse directamente en un dispositivo Android para enseñarla y probarla.

### 10. Cómo instalar el APK en un dispositivo Android

Una vez que tienes el APK, hay varias formas de pasar la aplicación al dispositivo:

* Descargarla directamente desde el enlace de EAS
* Enviarla por cable USB
* Subirla a Google Drive y descargarla en el dispositivo
* Enviarla por correo, Telegram o WhatsApp si el tamaño lo permite

Al abrir el APK en el dispositivo, Android puede mostrar un aviso indicando que no se permite instalar aplicaciones de fuentes desconocidas.

En ese caso, debes hacer lo siguiente:

1. Ir a **Ajustes**.
2. Entrar en **Seguridad** o **Privacidad**.
3. Buscar la opción **Instalar aplicaciones desconocidas**.
4. Dar permiso al navegador, gestor de archivos o aplicación desde la que se abra el APK.
5. Volver al archivo APK.
6. Pulsar en **Instalar**.

Cuando termine la instalación, la aplicación aparecerá en el dispositivo como una aplicación normal.

### 11. Comandos principales usados

Estos fueron los comandos más importantes del proceso. Primero, la preparación inicial:

```powershell

npm install -g eas-cli
eas login
eas build:configure

```

También revisé o instalé las dependencias necesarias para NativeWind y TailwindCSS:

```powershell

npm install nativewind react-native-reanimated react-native-safe-area-context

npm install --save-dev tailwindcss@^3.4.17 prettier-plugin-tailwindcss@^0.5.11 babel-preset-expo

```

Después, para generar la aplicación para la tienda de aplicaciones:

```powershell

eas build --platform android --profile production

```

Resultado esperado:

```txt

.aab

```

Para generar la aplicación instalable directamente:

```powershell

eas build --platform android --profile preview

```

Resultado esperado:

```txt

.apk

```

Para consultar las aplicaciones recientes:

```powershell

eas build:list --platform android

```

### 12. Notas finales

Durante el proceso, apareció un aviso sobre Expo Go. Ese aviso no bloquea la aplicación. Simplemente indica que, para una aplicación real, es mejor usar aplicaciones propias generadas con EAS.

También es importante no cambiar dependencias mientras una aplicación está en progreso, porque eso puede hacer que después no coincida el estado del proyecto local con el que se ha subido a EAS.

En mi caso, el flujo correcto quedó así:

```txt

1. Preparar dependencias.
2. Comprobar configuración de Expo.
3. Revisar TypeScript.
4. Generar .aab para la tienda de aplicaciones.
5. Generar .apk para instalación directa.
6. Probar el APK en un dispositivo Android.

```
