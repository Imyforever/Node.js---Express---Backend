# Backend API - Administrador de Tareas

API REST desarrollada con Node.js, Express y MongoDB (Mongoose) para la gestión y administración de tareas por usuario. Cuenta con autenticación mediante JSON Web Tokens (JWT) y protección de rutas con Bearer Token, garantizando que cada usuario únicamente pueda visualizar, registrar, actualizar y eliminar sus propias tareas.

---

## Características
* Registro e inicio de sesión de usuarios con contraseñas encriptadas mediante `bcrypt`.
* Generación y validación de tokens JWT (`Bearer Token`).
* CRUD completo de tareas protegido: cada usuario solo accede a sus tareas.
* Conexión a base de datos en la nube con MongoDB Atlas.

---

## Requisitos Previos
* [Node.js](https://nodejs.org/) (versión 18 o superior recomendada)
* [npm](https://www.npmjs.com/)
* Una cuenta o clúster configurado en [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)

---

## Instalación y Configuración

1. **Clonar el repositorio:**
   ```bash
   git clone <URL_DE_TU_REPOSITORIO>
   cd 2026backA
   ```

2. **Instalar dependencias:**
   ```bash
   npm install
   ```

3. **Configurar variables de entorno:**
   Crea un archivo `.env` en la raíz del proyecto basándote en `.env.example`:
   ```bash
   cp .env.example .env
   ```
   Define tus valores en el archivo `.env`:
   ```env
   PORT=5000
   NODE_ENV=development
   MONGO_DB=tu_cadena_de_conexion_mongodb
   JWT_SECRET=tu_clave_secreta_jwt
   ```

---

## Ejecución

* **Modo desarrollo (con recarga automática mediante Nodemon):**
  ```bash
  npm run server
  ```

* **Modo producción:**
  ```bash
  npm start
  ```

El servidor iniciará por defecto en `http://localhost:5000`.

---

## Lista de Endpoints

### 1. Usuarios (`/api/users`)

| Método | Endpoint | Acceso | Descripción | Body (JSON) |
|---|---|---|---|---|
| `POST` | `/api/users/register` | Público | Registra un nuevo usuario | `{"nombre": "...", "email": "...", "password": "..."}` |
| `POST` | `/api/users/login` | Público | Inicia sesión y retorna token JWT | `{"email": "...", "password": "..."}` |
| `GET` | `/api/users/datos` | Privado | Obtiene la información del usuario en sesión | *Ninguno* |

### 2. Tareas (`/api/tareas`)
> Todas las rutas de tareas requieren el header: `Authorization: Bearer <TOKEN_JWT>`

| Método | Endpoint | Acceso | Descripción | Body (JSON) |
|---|---|---|---|---|
| `GET` | `/api/tareas` | Privado | Obtiene todas las tareas del usuario autenticado | *Ninguno* |
| `POST` | `/api/tareas` | Privado | Crea una nueva tarea asociada al usuario | `{"descripcion": "..."}` |
| `PUT` | `/api/tareas/:id` | Privado | Actualiza una tarea propia existente | `{"descripcion": "..."}` |
| `DELETE` | `/api/tareas/:id` | Privado | Elimina una tarea propia | *Ninguno* |

