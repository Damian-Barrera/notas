
## Instalación

1. **Crear un proyecto Express**
   - Para crear un proyecto de Express, primero inicializa el proyecto con `npm init`:     npm init -y
    
   - Luego, instala Express:
      
     npm install express
     
   - Recordar que se debe agregar en el package.json la entrada que indique que se va a utilizar ESM y no common js. Puede ser debajo de "main" colocar "type" : "module", 


2. **Estructura Básica de un Servidor Express**
   - En el archivo principal de tu proyecto (por ejemplo, `app.js`), importa y configura Express:
 
     import express from 'express';
     const app = express();
     const port = 3000;

     app.get('/', (req, res) => {
       res.send('¡Hola Mundo!');
     });

     app.listen(port, () => {
       console.log(`Servidor corriendo en http://localhost:${port}`);
     });
     ```

3. **Para correr la aplicación**
   - Ejecuta el servidor con el comando:
      node app.js


## Variables de Entorno:

* Para acceder a las variables de entorno : 
    process.env.NOMBRE_DE_VARIABLE 
 
## Rutas

1. **Definir Rutas Básicas**
   - Define rutas con el método correspondiente (`app.get()`, `app.post()`, etc.):
    
      app.get('/ruta', (req, res) => {
       res.send('Respuesta a la ruta GET');
     });
     ```

2. **Rutas con Parámetros**
   - Para definir rutas con parámetros, usa `:param`:
 
      app.get('/saludar/:nombre', (req, res) => {
       const nombre = req.params.nombre;
       res.send(`Hola, ${nombre}`);
     });
     ```

3. **Redirigir a otra Ruta**
   - Para redirigir a otra ruta:
     ```javascript
     app.get('/redirigir', (req, res) => {
       res.redirect('/');
     });
     ```

## Middleware

1. **Middleware Básico**
   - Express usa middlewares para manejar solicitudes antes de que lleguen a las rutas. Puedes usar `app.use()` para aplicar middlewares globalmente:
     ```javascript
     app.use((req, res, next) => {
       console.log('Solicitud recibida');
       next(); // Asegura que la solicitud siga al siguiente middleware o ruta
     });
     ```

2. **Middleware de JSON**
   - Para manejar cuerpos de solicitud en formato JSON:
     ```javascript
     app.use(express.json());
     ```

3. **Middleware Estático**
   - Para servir archivos estáticos (como imágenes, CSS, etc.):
     ```javascript
     app.use(express.static('public'));
     ```

## Envío de Datos

1. **Enviar Respuestas en JSON**
   - Puedes responder con datos en formato JSON:
     ```javascript
     app.get('/datos', (req, res) => {
       res.json({ mensaje: 'Aquí están tus datos' });
     });
     ```

2. **Recibir Datos del Cuerpo de la Solicitud**
   - Para manejar datos enviados en una solicitud `POST` (usando `express.json()`):
     ```javascript
     app.post('/guardar', (req, res) => {
       const { nombre, edad } = req.body;
       res.send(`Recibido: ${nombre}, Edad: ${edad}`);
     });
     ```

## Manejo de Errores

1. **Manejo de Errores**
   - Puedes manejar errores utilizando un middleware de error:
     ```javascript
     app.use((err, req, res, next) => {
       console.error(err);
       res.status(500).send('Hubo un error en el servidor');
     });
     ```

2. **Capturar Errores 404**
   - Para capturar rutas no encontradas:
     ```javascript
     app.use((req, res) => {
       res.status(404).send('Ruta no encontrada');
     });
     ```

## Variables de Entorno

1. **Uso de Variables de Entorno**
   - Para usar variables de entorno, crea un archivo `.env` y usa el paquete `dotenv`:
     ```bash
     npm install dotenv
     ```
     - En el archivo `.env`:
       ```
       PORT=3000
       ```
     - En `app.js`:
       ```javascript
       import dotenv from 'dotenv';
       dotenv.config();
       const port = process.env.PORT || 3000;
       ```

## Conexión a Base de Datos

1. **Conectar con MongoDB (Mongoose)**
   - Instala `mongoose` para conectarte a MongoDB:
     ```bash
     npm install mongoose
     ```
   - Enlaza la base de datos:
     ```javascript
     import mongoose from 'mongoose';
     mongoose.connect('mongodb://localhost/mi_base_de_datos', { useNewUrlParser: true, useUnifiedTopology: true })
       .then(() => console.log('Conectado a MongoDB'))
       .catch(err => console.log('Error al conectar a MongoDB', err));
     ```

2. **Definir un Modelo**
   - Define un modelo para interactuar con la base de datos:
     ```javascript
     const usuarioSchema = new mongoose.Schema({
       nombre: String,
       edad: Number,
     });
     const Usuario = mongoose.model('Usuario', usuarioSchema);
     ```

---

## Resumen de Comandos Útiles

- `npm init -y` - Inicializa un proyecto Node.js
- `npm install express` - Instala Express
- `node app.js` - Ejecuta el servidor
- `app.get('/ruta')` - Define una ruta GET
- `app.post('/ruta')` - Define una ruta POST
- `app.use(express.json())` - Usa el middleware para JSON
- `app.use(express.static('public'))` - Sirve archivos estáticos
- `import dotenv from 'dotenv'; dotenv.config()` - Carga variables de entorno
