# Agenda de citas · Eleganza Academia

Esta carpeta tiene todo lo necesario para publicar la agenda en internet, con base de datos propia y acceso con usuario y contraseña.

- `index.html`: la aplicación.
- `firestore.rules`: las reglas de seguridad de la base de datos.

La base de datos y los usuarios quedan en **Firebase** (de Google). La página se publica gratis en **Netlify**. Para el uso de un equipo como este, el plan gratuito de ambos es suficiente.

## 1. Crear el proyecto en Firebase

1. Entra a https://console.firebase.google.com con una cuenta de Google de la empresa.
2. Toca **Crear un proyecto**, ponle un nombre (por ejemplo `eleganza-agenda`) y termina el asistente. Puedes desactivar Google Analytics.

## 2. Activar la base de datos

1. En el menú izquierdo: **Compilación → Firestore Database → Crear base de datos**.
2. Ubicación: elige una cercana, por ejemplo `southamerica-east1 (São Paulo)` o `us-east1`. **No se puede cambiar después.**
3. Elige **Iniciar en modo de producción**.
4. Abre la pestaña **Reglas**, borra todo, pega el contenido del archivo `firestore.rules` y toca **Publicar**.

## 3. Activar el inicio de sesión

1. Menú: **Compilación → Authentication → Comenzar**.
2. En **Método de acceso**, activa **Correo electrónico/contraseña** (solo la primera opción) y guarda.
3. En **Configuración → Acciones del usuario**, desmarca **Habilitar la creación (registro)**. Así nadie puede crearse una cuenta por su cuenta: solo tú creas los usuarios.
4. En la pestaña **Usuarios**, toca **Agregar usuario** y crea uno por cada persona que va a agendar (correo y contraseña temporal).

> Cada persona puede cambiar su contraseña desde la pantalla de ingreso con "Olvidé mi contraseña".

## 4. Conectar la app con tu proyecto

1. En Firebase, toca el engranaje ⚙️ → **Configuración del proyecto**.
2. En **Tus apps**, toca el ícono **</>** (Web), ponle un nombre y registra la app (no marques Firebase Hosting).
3. Aparece un bloque `const firebaseConfig = { apiKey: ..., authDomain: ..., ... }`.
4. Abre `index.html` con el Bloc de notas (clic derecho → Abrir con → Bloc de notas), busca `PEGA AQUÍ LOS DATOS` y reemplaza los seis valores de `window.FIREBASE_CONFIG` con los de tu proyecto. Guarda el archivo.

> Esos datos no son secretos: lo que protege la información son las reglas del paso 2 y el inicio de sesión.

## 5. Publicar la página

1. Crea una cuenta gratis en https://app.netlify.com.
2. Ve a **Sites → Add new site → Deploy manually** y arrastra **la carpeta completa** (con `index.html` dentro).
3. Netlify te da un enlace tipo `https://algo.netlify.app`. Puedes cambiar el nombre en **Site configuration → Change site name** (por ejemplo `eleganza-agenda.netlify.app`).
4. En Firebase → **Authentication → Configuración → Dominios autorizados**, agrega ese dominio.

Comparte el enlace con tu equipo. Cada persona entra con su correo y contraseña.

## 6. Primer ingreso

La primera vez que alguien entra, la app crea automáticamente los 8 equipos: Suba, Soacha, Fontibón, Pasto, Kennedy, Chapinero, Zipaquirá y Venecia. Luego, en cada equipo, agrega a las personas que atienden citas.

## Copias de seguridad

Los datos quedan guardados en Firestore. Puedes verlos en **Firestore Database → Datos** (colecciones `citas` y `config`). Para respaldos automáticos, Firebase ofrece exportaciones programadas en el plan de pago (Blaze); para empezar no es necesario.

## Actualizar la app más adelante

Si cambias `index.html`, entra a tu sitio en Netlify → **Deploys** y arrastra de nuevo la carpeta. Las citas no se pierden, porque viven en Firebase y no en el archivo.
