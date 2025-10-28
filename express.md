## Instalación

1. **Crear un proyecto Express**

   - Para crear un proyecto de Express, primero inicializa el proyecto con `npm init`: npm init -y

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

     ```

3. **Para correr la aplicación**
   - Ejecuta el servidor con el comando:
     node app.js

## Variables de Entorno:

- Para acceder a las variables de entorno :
  process.env.NOMBRE_DE_VARIABLE //NO OLVIDAR QUE LAS VARIABLES DE ENTORNO VAN EN MAYUSCULAS.

## Rutas

1. **Definir Rutas Básicas**

   -app.use(express.static('.')); Este middleware es importante ya que ayuda a decirle a express cual es el inicio de la aplicacion. Si no se usa puede tener problemas a la hora de cargar archivos de css o imagenes u otros archivos js.

   - Define rutas con el método correspondiente (`app.get()`, `app.post()`, etc.):

     app.get('/ruta', (req, res) => {
     res.send('Respuesta a la ruta GET');
     });

    

2. **Rutas con Parámetros**

   - Para definir rutas con parámetros, usa `:param`:

     app.get('/saludar/:nombre', (req, res) => {
     const nombre = req.params.nombre;
     res.send(`Hola, ${nombre}`);
     });

     ```

     ```

3. **Redirigir a otra Ruta**

   - Para redirigir a otra ruta:
     ```javascript
     app.get("/redirigir", (req, res) => {
       res.redirect("/");
     });
     ```

4. **Routers**
   // Los routers sirven para organizar rutas y mantener el código modular.

// Inicializamos Express:
const app = express();

// Definimos el Router (uno por grupo de rutas):
const miRouter = express.Router();

// Asociamos el router a una ruta base:
app.use('/aqui/va/la/ruta/que/hace/referencia', miRouter);

// Dentro del router, definimos las rutas relativas:
miRouter.get('/', (req, res) => {
res.send('Aquí lo que se enviará');
});

// También se pueden usar parámetros como en rutas normales:
miRouter.get('/:elParametro', (req, res) => {
res.send(`El parámetro recibido es: ${req.params.elParametro}`);
});

## Middleware

1. **Middleware Básico**

   - Express usa middlewares para manejar solicitudes antes de que lleguen a las rutas. Puedes usar `app.use()` para aplicar middlewares globalmente:
     ```javascript
     app.use((req, res, next) => {
       console.log("Solicitud recibida");
       next(); // Asegura que la solicitud siga al siguiente middleware o ruta
     });
     ```

2. **Middleware de JSON**

   - Para manejar cuerpos de solicitud en formato JSON:
      app.use(express.json());
 
3. **Middleware Estático**
   - Para servir archivos estáticos (como imágenes, CSS, etc.):
      app.use(express.static("public"));
 
## Envío de Datos

1. **Enviar Respuestas en JSON**

   - Puedes responder con datos en formato JSON:
     ```javascript
     app.get("/datos", (req, res) => {
       res.json({ mensaje: "Aquí están tus datos" });
     });
     ```

2. **Recibir Datos del Cuerpo de la Solicitud**
   - Para manejar datos enviados en una solicitud `POST` (usando `express.json()`):
     ```javascript
     app.post("/guardar", (req, res) => {
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
       res.status(500).send("Hubo un error en el servidor");
     });
     ```

2. **Capturar Errores 404**
   - Para capturar rutas no encontradas:
     ```javascript
     app.use((req, res) => {
       res.status(404).send("Ruta no encontrada");INSERT INTO usuarios (nombre, apellido, email, password, is_admin) VALUES
('Juan', 'Pérez', 'juan@example.com', 'clave123', false),
('María', 'Gómez', 'maria@example.com', 'clave456', false),
('Luis', 'Martínez', 'luis@example.com', 'clave789', false),
('Ana', 'Fernández', 'ana@example.com', 'clave321', false),
('Carlos', 'López', 'carlos@example.com', 'clave654', false),
('Lucía', 'Ramírez', 'lucia@example.com', 'clave987', false),
('Pedro', 'Sánchez', 'pedro@example.com', 'clave147', false),
('Sofía', 'Torres', 'sofia@example.com', 'clave258', false),
('Diego', 'Ruiz', 'diego@example.com', 'clave369', false),
('Valeria', 'Morales', 'valeria@example.com', 'clave159', false);

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
       import dotenv from "dotenv";
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
     import mongoose from "mongoose";
     mongoose
       .connect("mongodb://localhost/mi_base_de_datos", {
         useNewUrlParser: true,
         useUnifiedTopology: true,
       })
       .then(() => console.log("Conectado a MongoDB"))
       .catch((err) => console.log("Error al conectar a MongoDB", err));
     ```

2. **Definir un Modelo**
   - Define un modelo para interactuar con la base de datos:
     ```javascript
     const usuarioSchema = new mongoose.Schema({
       nombre: String,
       edad: Number,
     });
     const Usuario = mongoose.model("Usuario", usuarioSchema);
     ```

---

### Base de datos:

-Se puede usar mysql instalando desde npm mysql2 .
-Luego desde el codigo importarla :
import mysql from 'mysql2/promise' ;
-Despues, crear la configuracion con los parametros de host, user,puerto, password y base de datos.

    const config = {
      host : 'localhost',
      user : 'root',
      puerto : 3306, //Ver cual es el puerto que nos de el gestor de base de datos.
      password : '',
      database : 'nombre_de_la_base_de_datos'
    }

-Finalmente, hacemos la conexion pasando como parametro la variable, con los datos de la conexion.
const connection = await mysql.createConnection(config)

- Para insertar datos a la base de datos :
  const query = 'INSERT INTO usuarios (nombre, apellido, email) VALUES (?, ?, ?)';
  //La manera mas segura de escapar caracteres especiales es usando los signos de interrogacion.
  // Se deben haber creado las variables previamente o provenir de un formulario u otro lado.
  const [resultado] = await connection.execute(query, [nombre, apellido, email]);
  await connection.end();

*** Uso del pool
-El uso de pool se hace para evitar tener que abrir y cerrar la conexion a la bd por cada consulta realizada evitando asi el consumo excesivo de recursos. La apaertura y cierre se hace de manera automatica. Lo que hace es abrir hasta cierta cantidad de conexiones(previamente definidas en la configuracion) y si estan ocupadas la conexion entrante debe esperar a que se libere alguna. 

          import mysql from "mysql2/promise";

          // Creamos el pool de conexiones
          const pool = mysql.createPool({
            host: "localhost",
            user: "root",        // tu usuario
            password: "", // tu contraseña
            database: "bd_pool",
            waitForConnections: true, // espera si no hay conexiones disponibles
            connectionLimit: 10, // máximo de conexiones simultáneas
            queueLimit: 0 // sin límite de espera
          });

// Exportamos el pool para usarlo en otras partes
export default pool;

-Luego en el archivo en donde haremos las consultas debemos llamar al pool:
import pool from 'ruta donde esta el archivo de configuracion'

  const [result] = await pool.query( aqui la consulta a la DB )

  En el array [result] vienen agunos datos importantes: 
-affectedRows	  Saber si se modificó/eliminó alguna fila
-insertId	      Obtener el id generado en un INSERT
-changedRows	  Saber cuántas filas cambiaron realmente (UPDATE)
-warningStatus	Detectar advertencias de MySQL


### Formularios

-Para capturar datos de un formulario NO se debe enviar los datos en el action a un archivo html sino a una ruta del servidor. Por ejemplo no debo enviar a action="/misdatos.html" sino que debo hacerlo a action="/datos" .

-Habilitar el middleware para leer datos POST:
Express no puede leer los datos enviados en req.body si no usás el middleware correspondiente que es :
Debo declararlo antes de las rutas.  
 app.use(express.urlencoded({ extended: true }))

-La ruta que recibira los datos debe ser en POST . Ej:
app.post('/datos', (req, res) => {
Las variables que van a ser destructuradas son las que estan definidas en el name del input

    const { nombre, apellido, email } = req.body;
    console.log('Datos recibidos:', req.body); // para ver en consola

    res.send(`
        <h1>Datos recibidos</h1>
        <p>Nombre: ${nombre}</p>
        <p>Apellido: ${apellido}</p>
        <p>Email: ${email}</p>
        <a href="/">Volver</a>
    `);

});

-Para encriptar los datos se puede usar la libreria bcrypt.
npm install bcrypt
import bcrypt from 'bcrypt';

--hash() genera el hash de la contraseña.
--compare() compara el texto plano con el hash almacenado.
--saltRounds determina cuán fuerte es la encriptación (10 está bien por defecto).


const contraseñaPlano = 'mi_clave_segura';
const saltRounds = 10;

const hash = await bcrypt.hash(contraseñaPlano, saltRounds);
console.log('Contraseña encriptada:', hash);

\*\*Encriptar:
const saltRounds = 10;

const hash = await bcrypt.hash(contraseñaPlano, saltRounds);
console.log('Contraseña encriptada:', hash);

\*\* Para comparar :
const coincide = await bcrypt.compare('mi_clave_segura', hash);

if (coincide) {
console.log('Contraseña correcta');
} else {
console.log('Contraseña incorrecta');
}


### Cargar Imagenes 
-No olvidar que para poder trabajar desde rutas post debo usarl el middelware:  
  app.use(express.urlencoded({ extended: true }))
-El formulario debe usar enctype="multipart/form-data" . En caso de querer cargar varios archivos en el input file colocar el atributo multiple :
    <input type="file" name="imagenes" multiple />


-Para poder procesar imagenes se debe instalar multer. 
(si quiero hacer pruebas enviando solo datos sin las imagenes y sin el multer, me dara error al leer los name del html si tengo colocado el enctype.)


### Para ver datos de una base de datos :

-Tener en cuenta que para ver datos de una base de datos una manera es creando una api y consultarla con fecth. Al igual que si quiero ver los datos ingresados desde un formulario no se puede hacer de manera directa a travez de un html. Se debe hacer devolviendo e html con el objeto res.send() y dentro escribir el html. Otra manera de manejar datos de manera dinamica es usando un motor de plantillas ya sea handlebar, pug , ejs ,etc.

https://github.com/Damian-Barrera/aprendiendo_express.git


## Sessiones 
Primero instalar dependencias : 
npm install express-session


Luego se hace la configuracion basica: 
import session from "express-session";

// Configuración de session
app.use(session({
  secret: "mi_clave_secreta", // clave para firmar la cookie
  resave: false,              // no guardar sesión si no hay cambios
  saveUninitialized: true,    // guardar sesiones nuevas aunque no tengan datos
  rolling: true, //  renueva la expiración en cada request.Esto hace que la sesion se actualize mientras el usuario este activo.
  cookie: { maxAge: 1000 * 60 * 60 } // duración de la cookie: 1 hora
}));

# Notas sobre la configuración:

secret: se usa para firmar la cookie, debe mantenerse privada.

resave: false para no escribir en el servidor si no hubo cambios.

saveUninitialized: true permite crear sesiones vacías (útil para pruebas; en producción suele ponerse false).

rolling: útil para extender la sesión si el usuario sigue activo.

cookie.maxAge: define cuánto dura la sesión sin actividad.

# Crear / guardar datos en la sesion
// Después de un login exitoso
req.session.user = {
  id: 1,
  nombre: "Damian",
  is_admin: 1
};
user es un nombre elegido por uno mismo, podría llamarse de cualquier manera (req.session.usuario, req.session.auth, etc.).

Todos los datos guardados en req.session persisten mientras dure la sesión.

# Acceder a la sesión
app.get("/dashboard", (req, res) => {
  if (!req.session.user) {
    return res.redirect("/"); // si no hay sesión, ir al login
  }

  console.log(req.session.user.nombre); // acceder a datos del usuario
});

# Destruir la sesión (logout)
app.get("/logout", (req, res) => {
  req.session.destroy(err => {
    if (err) return res.send("Error al cerrar sesión");
    res.redirect("/"); // vuelve al login
  });
});

# Uso con HTML estático y fetch

Si se quiere mostrar datos dinámicos en un HTML estático, lo más práctico es crear un endpoint API:

app.get("/api/user", (req, res) => {
  if (!req.session.user) return res.status(401).json({ error: "No autenticado" });
  res.json(req.session.user);
});

** Y crear un script (js) vinculandolo al html : 

<script>
fetch("/api/user")
  .then(res => res.json())
  .then(user => {
    document.getElementById("nombreUsuario").textContent = user.nombre;
  })
  .catch(() => window.location.href = "/"); // redirige si no hay sesión
</script>
*En los formularios de inicio de sesion, se debe capturar el evento submit, prevenir el eventDefault y hacer el fetch post, con los datos que debieron haber sido capturados del formulario, al endpoint definido en el index del backend.

## Resumen de Comandos Útiles

- `npm init -y` - Inicializa un proyecto Node.js
- `npm install express` - Instala Express
- `node app.js` - Ejecuta el servidor
- `app.get('/ruta')` - Define una ruta GET
- `app.post('/ruta')` - Define una ruta POST
- `app.use(express.json())` - Usa el middleware para JSON
- `app.use(express.static('public'))` - Sirve archivos estáticos
- `import dotenv from 'dotenv'; dotenv.config()` - Carga variables de entorno
