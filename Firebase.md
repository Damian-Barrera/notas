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