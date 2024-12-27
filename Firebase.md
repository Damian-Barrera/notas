-Recordar que todas las consultas a firestore son asincronas, por lo que las consultas deben estar encerradas en una funcion asincrona es decor con asyn/await y tambien es recomendable que estas esten encerradas en un try catch . 

## Comandos para usar firebase

-Antes que nada se debe de crear el proyecto en firebase, ya que luego se necesitaran archivos de configuracion con datos que se obtendran del proyecto creado y que van a ser proporcionados por firebase.
-Hay una seccion para registrar la app. Sino no me creara el archivo de configuracion.
-Luego se debera crear un archivo de configuracion (un simple js) con los siguientes datos:(se obtienen del proyecto en firebase, en la parte de configuracion esta el codigo necesario)

        import { initializeApp } from "firebase/app";
        
        import { getFirestore } from '@firebase/firestore'

        const firebaseConfig = {
            Este objeto me lo proporciona firestore con los datos de mi app
        };

        // Iniciar Firebase
        const app = initializeApp(firebaseConfig);
        export const db = getFirestore(app) 

-Se debe importar firebase 
-Se debe importar la base de datos, db , que es la que se creo en el archivo js.
-Tambien los modulos de firestore que van a ser usados: collection, getDocs, addDoc, deleteDoc,doc,getDoc, updateDoc. Cada uno se importara en el componente que vayan a ser usados.  

## Metodos de firestore:
** Recordar que los id en firestore se pueden crear de forma automatica.

-collection(baseDeDatos, 'nombreColleccion') : Recibe dos parametros. El nombre de la base de datos, que es la que esta definida en el archivo js y el otro parametro es el nombre de la coleccion 

-getDocs(coleccionReferencia): Recibe un solo parametro, que es la referencia a la coleccion que se definio anteriormente. Esta coleccion trae como datos el nombre de la base de datos y el nombre de la coleccion.

-doc(baseDatos,'coleccion','id'): Recibe tres parametros. El primero es la base de datos. El segundo es el nombre de la collecion y el tercero es el id del documento al que hacer referencia.


-getDoc(documentoReferencia): Recibe un parametro que es el resultado de doc que trae tres datos que eran base datos, coleccion y el id. 

-addDoc(collectionRef, {datos}) : Recibe dos parametros. El primero es la coleccion o la referencia a la coleccion. Y el segundo es un objeto con los datos que se quieren agegar a la coleccion.


-setDoc(documentoReferencia, {datos}) : Recibe dos parametros, El primero es el resultado de doc.Que me traia tres datos. y el segundo un objeto con los datos que quiero modificar. Si el documento ya existe lo sobrescribe y si no existe lo crea.

-updateDoc(docRef, {data}): Recibe dos parametros, el primero es el documento al que hace refencia, que es el resultado de doc(). Y el segundo un objeto con los campos que quiero actualizar. Solo modifica los campos indicados. Este metodo es el que deberia usar en caso de querer agregar un campo a un documento. Ya que al agregar el campo no modifica los anteriores.

-deleteDoc(docRef): Recibe un parametro que es el resultado de doc().

-onSnapshot(docRef, callback): Recibe dos parametros. El primero es el resultado de collection o doc. Permite escuchar cambios en tiempo real. Y el segundo es una función que se ejecuta cada vez que hay un cambio en la colección o documento.
Es util para mostrar cambios en tiempo real ya que la consulta a la base de datos se realiza mas rapido debido a que solo envia la informacion que se modifico y recibe como respuesta el o los datos modificados evitando asi que haya un trafico innecesario de datos.

****************************************************************************************.
#### Firebase Authentication 
-Se deben importar en el archivo de configuracion getAuth y GoogleAuthProvider (para logearse con google) desde firebase/auth


-1. createUserWithEmailAndPassword( auth, email, password ) : Crea un nuevo usuario con correo electrónico y contraseña.

Parámetros:
auth: La instancia de autenticación.
email: El correo electrónico del usuario.
password: La contraseña del usuario.

 *Firebase maneja los errores de manera interna. Si coloco este metodo dentro de un try catch puedo hacer un console.log del error y alli me dira el tipo de error. Para hacerlo de manera mas especifica hacer el console.log de error.code y alli me dira el tipo  de error para luego poder tratarlo a travez de validaciones y asi lanzar alertas al usuario sobre el error. Algunos errores que se pueden cometer son : email ha sido registrado, o mal formato del email, contraseña demasido corta (debe tener al menos 6 caracteres) 

-2. signInWithEmailAndPassword(auth, email, password): Permite que un usuario inicie sesión con su correo y contraseña.

Parámetros:
auth: La instancia de autenticación.
email: El correo electrónico del usuario.
password: La contraseña del usuario.


-3. signOut(auth): Cierra la sesión del usuario actualmente autenticado.

Parámetros:
auth: La instancia de autenticación.


-4. onAuthStateChanged(auth, callback): Escucha los cambios en el estado de autenticación (inicio o cierre de sesión).

Parámetros:
auth: La instancia de autenticación.
callback: Función que se ejecuta cuando el estado de autenticación cambia.
En el callback, que es una funcion asyncrona me devuelve el usuario si es que esta autenticado, sino me devuelve null.  


-5. sendPasswordResetEmail(auth, email): Envía un correo electrónico para que el usuario restablezca su contraseña.

Parámetros:
auth: La instancia de autenticación.
email: El correo electrónico del usuario.


-6. confirmPasswordReset(auth, code, newPassword): Confirma el cambio de contraseña usando un código enviado al correo electrónico.

Parámetros:
auth: La instancia de autenticación.
code: Código recibido en el correo para confirmar el restablecimiento.
newPassword: La nueva contraseña que se asignará.


-7. updatePassword(user, newPassword): Actualiza la contraseña del usuario actual.

Parámetros:
user: El objeto del usuario actualmente autenticado.
newPassword: La nueva contraseña del usuario.


-8 . updateEmail(user, newEmail): Actualiza el correo electrónico del usuario actual.

Parámetros:
user: El objeto del usuario actualmente autenticado.
newEmail: El nuevo correo electrónico.


-9. deleteUser(user): Elimina al usuario actualmente autenticado.

Parámetros:
user: El objeto del usuario actualmente autenticado.


-10. reauthenticateWithCredential(user, credential): Reautentica a un usuario con credenciales válidas (necesario para operaciones sensibles).

Parámetros:
user: El objeto del usuario actualmente autenticado.
credential: Las credenciales del usuario (por ejemplo, correo y contraseña).


-11. signInWithPopup(auth, provider): Inicia sesión con un proveedor de terceros usando una ventana emergente.

Parámetros:
auth: La instancia de autenticación.
provider: Proveedor de autenticación (como Google o Facebook).
*En el provider puede ser asi : 
                                            const provider = new GoogleAuthProvider()
                                            const provider = new FacebookAuthProvider()
                                            const provider = new GithubAuthProvider()
  

*En facebook hay que ir a facebook developer y configurar una nueva app. Cuando pregunte por la url del sitio colocar el localhost:numero_correspondiente (en caso de produccion). Cambiarlo cuando se tenga una url ya definida.
Luego en el menu de configurar ir a Acceso de OAuth de navegador insertado y colocarlo en si. En donde dice URI de redireccionamiento de OAuth validos, colocar el que me proporciona firebase en la pestaña donde activo todos los provedores de autenticacion. Luego volver a configurar e informacion basica. Alli me da el identificador de la aplicacion y la clave sercreta de la app que es la que se me pide en firebase.

*Para github es similar , quiza sea mas facil colocar en google github auth firebase o simiar , asi me da el enlace directo a la parte de configuracion para crear el id y id secreto.  

 
-12. signInWithRedirect(auth, provider): Inicia sesión con un proveedor de terceros redirigiendo al usuario.

Parámetros:
auth: La instancia de autenticación.
provider: Proveedor de autenticación (como Google o Facebook).


-13. getRedirectResult(auth): Recupera el resultado de una autenticación después de redirigir.

Parámetros:
auth: La instancia de autenticación.


-14. signInWithCredential(auth, credential): Autentica a un usuario usando credenciales específicas.

Parámetros:
auth: La instancia de autenticación.
credential: Las credenciales del usuario (como un token de acceso de un proveedor).


-15. signInAnonymously(auth): Inicia sesión de manera anónima sin registrar al usuario.

Parámetros:
auth: La instancia de autenticación.


-16. setPersistence(auth, persistence): Configura la persistencia de la sesión.

Parámetros:
auth: La instancia de autenticación.
persistence: Nivel de persistencia (local, session, none).


-17. getAuth(): Inicializa y recupera la instancia de autenticación de Firebase.

Parámetros:
No recibe parámetros.


-18. updateProfile(user, {displayName, photoURL}): Actualiza el perfil del usuario actual (nombre, foto, etc.).

Parámetros:
user: El objeto del usuario actualmente autenticado.
{displayName, photoURL}: Objeto con las propiedades del perfil a actualizar.


-19. verifyBeforeUpdateEmail(user, newEmail): Envía un correo para verificar el cambio de dirección de correo.

Parámetros:
user: El objeto del usuario actualmente autenticado.
newEmail: El nuevo correo electrónico a verificar.


-20. linkWithCredential(user, credential): Vincula un método de autenticación adicional a un usuario existente.

Parámetros:
user: El objeto del usuario actualmente autenticado.
credential: Las credenciales adicionales para vincular.