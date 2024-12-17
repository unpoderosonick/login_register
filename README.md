# Login_Register

Este es un proyecto de autenticación básico desarrollado con **Nuxt 3**, **Firebase** y **Tailwind CSS**. Proporciona funcionalidades para registrar usuarios, iniciar sesión y redirigir a una página de inicio después de la autenticación.

## Características

- Registro de usuarios con Firebase.
- Inicio de sesión y manejo de errores claros.
- Redirección a una página principal después de iniciar sesión.
- Uso de Tailwind CSS para el diseño responsivo.

## Requisitos

- **Node.js** versión 16 o superior.
- **Yarn** o **npm** para gestionar dependencias.
- Claves de configuración de un proyecto Firebase.

## Instalación

Sigue estos pasos para instalar y configurar el proyecto en tu entorno local:

### 1. Clona este repositorio

```bash
git clone https://github.com/tu-usuario/login_register.git
cd login_register


2. Instala las dependencias
Usa Yarn para instalar todas las dependencias necesarias:

bash
Copiar código
yarn install
3. Configura Firebase
Crea un archivo .env en la raíz del proyecto y agrega las claves de configuración de tu proyecto Firebase. El archivo debe tener el siguiente formato:

env
Copiar código
VITE_FIREBASE_API_KEY=TU_API_KEY
VITE_FIREBASE_AUTH_DOMAIN=TU_AUTH_DOMAIN
VITE_FIREBASE_PROJECT_ID=TU_PROJECT_ID
VITE_FIREBASE_STORAGE_BUCKET=TU_STORAGE_BUCKET
VITE_FIREBASE_MESSAGING_SENDER_ID=TU_MESSAGING_SENDER_ID
VITE_FIREBASE_APP_ID=TU_APP_ID
VITE_FIREBASE_MEASUREMENT_ID=TU_MEASUREMENT_ID
Reemplaza TU_API_KEY y otros valores con los datos de tu configuración de Firebase.

4. Ejecuta el proyecto
Inicia el servidor de desarrollo:

bash
Copiar código
yarn dev
Abre tu navegador y accede a http://localhost:3000.

Estructura del Proyecto
plaintext
Copiar código
login_register/
├── components/        # Componentes reutilizables
├── pages/             # Páginas del proyecto
│   ├── index.vue      # Página principal (opcional)
│   ├── login.vue      # Página de inicio de sesión
│   ├── register.vue   # Página de registro
│   └── home.vue       # Página principal después de iniciar sesión
├── public/            # Archivos públicos (imágenes, favicon, etc.)
├── assets/            # Archivos CSS y Tailwind
├── .env               # Configuración de claves (no incluido en el repositorio)
├── firebaseConfig.js  # Configuración de Firebase
├── nuxt.config.ts     # Configuración principal de Nuxt
└── README.md          # Este archivo
Uso
Registro
Accede a /register.
Completa los campos de correo y contraseña.
Haz clic en Registrar para crear un nuevo usuario.
Inicio de Sesión
Accede a /login.
Completa los campos de correo y contraseña.
Haz clic en Iniciar Sesión para iniciar sesión y ser redirigido a /home.
Página Principal
Después de iniciar sesión, serás redirigido automáticamente a /home.
Desde esta página puedes cerrar sesión para volver al inicio de sesión.
Tecnologías Utilizadas
Nuxt 3 - Framework para aplicaciones Vue.
Firebase - Backend-as-a-Service para autenticación y base de datos.
Tailwind CSS - Framework CSS utilitario.
Personalización
Si deseas personalizar el diseño, edita el archivo tailwind.config.js para agregar o modificar estilos. También puedes añadir componentes en la carpeta components/.

