-La variable global en Node no es window como en javascript sino globalThis .

-Para no tener que estar reiniciando la aplicacion cada vez que haya cambios: node --watch nombre_archivo_de_inicio

## Modulos Nativos

-OS : Sirve para recibir informacion del sistema operativo
const os = require('node:os)

                console.log(os.funcion()) En funcion se puede colocar una de las tantas variedades que ofrece node .(Presionar ctrl mas barra para las opciones.)

-fs : File System . Se usa mucho para la carga de archivo.
****Todos los modulos fs trabajan por defecto de manera asincrona. pero tiene su forma sincrona. Solo se le debe agregar el sync a final del nombre del metodo . Ej: readFileSync. 


    //Para leer archivos se usa:
      *fs.readFile('ruta_del_archivo', 'codificacion', callback)
       fs.readFile('index.htm', 'utf-8', (err, contenido )=>{
        if(err){
            console.log(err)
        }else{
            console.log(contenido)
        }
       })
    //Cambia el nombre de un archivo
    *fs.rename('ubicacion_del_archivo', 'nuevo_nombre_de_archivo', callback)
        fs.rename('index.html', 'main.html', (err) => {
            if(err){
                throw err
            }
        })
     //Agregar contenido a un archivo al final del archivo.Si no existe lo crea.   
     *fs.appendFile('nombre_del_archivo', 'contenido a agregar',callback)   

    //Reemplaza todo el contenido de un archivo
    *fs.writeFile(archivo viejo, archivo nuevo, callback)

    //Eliminar archivos
    *fs.unlink(nombre_archivo, callback)
    fs.unlink('index.html', (err)=>{
        if(err){
            throw err
        }
        console.log('archivo eliminado')
    })



-path : Sirve para construir rutas u obtener rutas.

-http: Modulo para crear el servidor . 

    const http = requiere('http')
    const servidor = http.createServer( (req,res) => {
        res.end('respuesta que se enviara')
    } )

    servidor.listen(puertoEnDondeSeEjecuta, ()=> {
        mesanje que se enviara.
    })

## Metodos de http
✅ listen
– Inicia el servidor y lo pone a la escucha.

✅ close
– Detiene el servidor.

✅ address
– Devuelve información sobre el puerto/IP donde está escuchando.

✅ getConnections
– Devuelve el número de conexiones activas.

✅ setTimeout
– Configura el tiempo de espera para las solicitudes.

✅ maxHeadersCount (propiedad, no método)
– Número máximo de cabeceras permitidas por solicitud.

// Escuchar en el puerto 3000
servidor.listen(3000, () => {
  console.log('Servidor escuchando en el puerto 3000.');

  // Mostrar la dirección y puerto donde está escuchando
  const addressInfo = servidor.address();
  console.log('Dirección del servidor:', addressInfo);

  // Configurar el tiempo de espera para las solicitudes (5 segundos)
  servidor.setTimeout(5000, () => {
    console.log('Se alcanzó el tiempo de espera de la solicitud.');
  });

  // Contar las conexiones activas
  servidor.getConnections((err, count) => {
    if (err) throw err;
    console.log('Conexiones activas:', count);
  });

  // Cerrar el servidor (en este ejemplo, lo hago inmediatamente)
  servidor.close(() => {
    console.log('Servidor cerrado.');
  });
-https

-URL : Este modulo sirve para trabajar con la url y extraer sus parametros..
    const miUrl = new URL('https://www.paginaweb.com/ruta/otraRuta')

    Algunos metodos: 
    miUrl.hostname 
    miUrl.pathName
    miUrl.searchParams //Este devuelve un objeto con su clave -valor . Se puede accedere a su valor con  el metodo get('clave')
        miUrl.searchParams().get('claveQueSeQuiereObtener')

-process : Este modulo provee informacion sobre el proceso que se esta ejecutando en node.

-timers : Sirve para simular operaciones asincronas. Contiene funciones que ejecutan codigo luego de cierto periodo de tiempo.
*setTimeOut(funcion, retraso, argumento)
*setImmediate(funcion, argumento1): La funcion se ejecutara despues del codigo sincrono. Tiene como cierta prioridad, se ejecutara inmediatamente cuando sea posible.
\*setInterval(funcion, intervalo, argumento1): Ejecuta codigo infinitamente, cada cierto periodo especificado.

-Events : Es un modulo que permite crear escuchar y manejar eventos personalizados. Este modulo exporta una case llamada EventEmmiter.

Se debe importar el modulo: const EventEmmiter = require('events')
const emisorProductos = new EventEmmiter();
emisorProductos.on('compra', (total) => {
    console.log(se realizao una compra por ${total})
})

emisorProductos.emit('compra', 500);

*Funciones principales :
-nombreEvento.on(evento, callback)
    Registra un listener para el evento.
-nombreEvento.emit(evento, [datos])
    Dispara (emite) el evento y pasa datos opcionales.
-nombreEvento.once(evento, callback)
    Igual que .on(), pero solo se ejecuta una vez.
-nombreEvento.removeListener(evento, callback) o .off()
    Elimina un listener.


 ### Otras librerias: 

 -crypto : Sirve para poder generar id unicos . Esta de forma nativa en node y se la debe importar .
 const crypto = import from 'crypto'
 id = crypto.randomUUID()  //Esto me generara un id unico. 

 
 
    