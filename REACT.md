-Para crear un proyeto se hace con npm create vite . Ir siguiendo las opciones.
-Luego de eso , entrar a la carpeta que se crea y alli instalar: npm install o npm i.
-Para correr la aplicacion, npm run dev .
-npm run build : Para empaquetar el proyecto y dejarlo listo para produccion.

## PROPS

-Para usar una props se puede hacer destructurando o anteponiendo la palabra props

export const NombreComponente = ( props ) => { //Aqui se abtepone la palabra props
return (

<div> props.nombreProps </div>
)
}

export const NombreComponente = ( {NombreProps}) => { //Aqui se desestructura la props
return (

<div> {nombreProps} </div>
)
}

-Recordar que cada vez que se use un map debe llevar una key, que es como un id que si no esta presente tira error.

************************

  ### Rutas

-Instalar e importar el react-router-dom

- En la aplicacion principal importar el browserRouter
  import { BrowserRouter } from 'react-router-dom'

    <BrowserRouter >
     <StrictMode>
         <App />
     </StrictMode>
   </BrowserRouter>,

  -Luego crear las rutas. Para ello debo: import {Routes, Route,Navigate} from 'react-router-dom
  -El navigate se usara para que la aplicacion, en caso de que se ingrese una ruta incorrecta me redirija a donde se le indique.

     <Routes>
         <Route path='palabra_que_referenciara' element= { <NombreComponente/> } > </Route>  
         <Route path='/*' element={ <Navigate to='/' /> } ></Route> En este caso se redirije al la raiz.
     </Routes>

  Ejemplo :
  <Routes>
  <Route path='/' element='' ></Route>
  <Route path='departamentos' element={<Departamentos />} > </Route>
  <Route path='empresa' element={<Empresa />} ></Route>
  <Route path='inicio' element={<Inicio />}></Route>
  <Route path='/\*' element={<Navigate to='/' />} ></Route> //Esta es la linea que maneja las rutas que no coinciden con 
  ninguna otra.
  </Routes>

-Y en el menu de navegacion : import {NavLink, Link} from 'react-router-dom
<NavLink to='lugarDondeLlevara'> Palabra que mostrara </NavLink>

Ejemplo:
<NavLink to="departamentos" > Departamentos </NavLink>

   <Link to="http://www.google.com" > Google! </Link>

-Todas las rutas deben ser declaradas en Routes. Y este a la vez puede ser un componente aparte, para asi poder tener un mejor 
control y organizacion de las rutas.

## Boton de volver atras

-Importar el useNavigate de react-router-dom
-crear una funcion que contenga el useState: const navigate = useNavigate()
-Crear una funcion manejadora del onClick cuyo contenido sera la funcion antes creada que tendra como parametro -1 . (Esto hace 
que la pagina regrese atras). (Estas dos funciones colocarlas dentro de la funcion del componente antes del return . )
const handleBack = () => {navigate(-1) }
-Luego llamar a la funcion que puede ser en un button, o icono, o lo que sea, con onClick
<button onClick={handleBAck} > <button>

## Enviar informacion de hijos a padres:

 -Para que un componente hijo envíe datos a su padre, debe existir un componente padre que envuelva a los hijos que se van
  a comunicar. El flujo de información va del hijo al padre mediante funciones que el componente padre pasa como props a los hijos.

-En el componente hijo, definimos una función interna que se encargará de invocar la función recibida desde el padre mediante 
props. Esta función se usa para enviar los datos hacia el padre.

export const Hijo1 = ({enviandoInformacion }) => {

    const enviarInfo = () => {
      enviandoInformacion('Todo esta ok!' )
    }
    return (
      <>
        <button onClick= { enviarInfo } > Obtener informacion! </button>
      </>
    )
}

-En el componente padre, declaramos una función que recibirá los datos enviados por el hijo. Esta función se pasa como prop 
al hijo para que pueda ser invocada desde allí. El componente padre también puede compartir el estado actualizado con otros 
hijos mediante props.

function App() {

 const [msg, setMsg] = useState('') 

const enviandoInformacion = (mensaje) => {
  setMsg( mensaje )
}

  return (
    <>
      <Hijo1 enviandoInformacion={enviandoInformacion} />
      <Hijo2 mensaje= {msg} />
    </>
  )
}

export default App

# Hooks 
***************

## useState

const [ estado, setEstado ] = useState('') 

-El set estado es el que modifica al estado. Y a la vez es el estado actual dentro del useState(''). El useState('') puede contener 
un string, array u objeto tambien. useState([]). useState({}), useState('')

-El set estado es una funcion : setEstado( codigo que modificara el estado )
-Si al set se le pasa un callback que contiene un parametro, este parametro representaria al estado actual del useState . 
  useEstad( (estadoActual) => modificar el estadoActual )

## useEffect

useEffect( () => {
Codigo que se ejecutara.
}, Lista de dependencias )

-Si en las "Listas de dependencias " No hay nada. El codigo se ejecutara todas las veces que el componente al que pertenece 
el hook se renderize
-Si se coloca un array vacio, [], El codigo se ejecutara solo una vez que sera cuando se renderiza el componente por primera vez .
-Si se coloca en el array un valor, el codigo se ejecutara cada vez que en ese "valor" (o mas valores) se produzcan cambios.

-Se suele usar un return dentro del useEffect que sirve para ejecutar codigo en caso de que se desmonte el componente: Un 
componente se desmonta
cada vez que ese componente cambia o sale de la vista de usuario. Entonces el codigo que hay dentro de return es el que se 
ejecutara. 


## useContext

-Este hook sirve para pasar datos entre varios componentes sin tener que pasar props de uno en uno.

-Puedo crear un componente aparte para crear la funcion que va a iniciar el contexto. Este componente puede ser un simple
archivo js.
import { createContext } from 'react'
const NombreFuncion = createContext(); Este nombre de funcion se recomienda iniciar con mayuscula.

-En el app.jsx o en el archivo padre donde engloba a los distintos componentes que usaran el contexto, se debe llamar a la
 funcion antes creada y asignarle el provider y el valor que usaran los hijos. Todos los componentes que esten dentro del
 Provider son los que podran tener acceso a los datos que se envien.

import {NombreFuncion} from 'ruta_donde_esté'

<NombreFuncion.Provider value= {valor_que_se_le_pasara}>

Ejemplo:

                  function App() {
                  const user = {nombre:'Damian', edad: 37}

                    return (
                      <>
                        <h1>UseContext</h1>
                        <UsuarioContext.Provider  value= {user}>
                          <Perfil />
                        </UsuarioContext.Provider>
                      </>
                    )
                  }

- Ya dentro del/los componente que usara el contexto se importara el useContext y a funcion que tiene el contexto.
  import {useContext} from 'react'
  import {NombreFuncion} from 'ruta.js'

- Y se llama al contexto :
  const variable = useContext( NombreFuncion )

-Dentro del return hago uso de esa variable:
return (
Hola, yo soy el contexto: {variable} En caso de que sea un objeto : variable.dato1
)

## useRef
-Este hook se usa para hacerreferencia a algun elemento html y manipularo sin esperar que se produzca un nuevo renderizado.
-Importar el useRef de React.
-Crear la referencia en una variable:
const nombreReferencia = useRef();

-Luego en el elemento al que se le va a hacer la referencia colocar el atributo ref con el nombre de la referencia (que fue 
la que se creo en la variable que contiene al useRef() )

<input ref={nombreReferencia} placeholder='algun texto'>

-Se debe crear la funcion que va a ejecutar el codigo deseado: Notar que el nombre de referencia se le debe agregar el "current".
const funcionLlamana = () => {
nombreReferencia.current.style.background='red'
}
Ejemplo:
function App() {

  const inputRef = useRef()
  const enfocar = () => {
       inputRef.current.style.backgroundColor='#cbff';
  }

  return (
        <>
         <h1>UseRef!</h1>
            <input type="text" name="" ref={inputRef} placeholder="Escribir aquí"/>
           <button onClick={enfocar} >Enfocar input</button>
          </>
  )
    }

## useMemo

-Este hook se utiliza cuando hay una funcion que maneja datos "pesados" o precisa de mucho calculo evitando que se vuelvan 
a renderizar los mismos a menos que cambien agunos valores que se le van a indicar. Su sintaxis es similar a la del useEffect. 

- EL useMemo es una funcion que recibe un callback como parametro y un array que es quien va a indicar las dependencias que 
van a hacer que se ejecute el codigo.


    const nombreFuncion = useMeno( () => {
        codigoAEjecutar ... 
    }, [dependencias])

  Ejemplo: 

function App() {
  const [contador, setContador] = useState(0);
  const [valor, setValor] = useState(100);

  ** useMemo memoriza el cálculo solo si 'valor' cambia

  const resultadoLento = useMemo(() => {
    console.log('Calculando...');
    return valor * 2;
  }, [valor]);

  return (
    <div>
      <h1>Contador: {contador}</h1>
      <button onClick={() => setContador(contador + 1)}>Incrementar</button>

        <h2>Resultado: {resultadoLento}</h2>
      <button onClick={() => setValor(valor + 10)}>Actualizar valor</button>
    </div>
  );
}


## useReduce 
-Sirve para manejar estados, para cuando una aplicacion empieza a crecer y el uso de useState puede volverse medio complejo .

import useReducer from 'react';

-Se debe crear la funcion reductora. Esta es la que va a llevar a cabo la ejecucion del codigo principal. 
-Recibe dos parametros: el estado y la accion. 

               const funcionReductora = (state, action) => {
                  witch (action) {
                    case 'INCREMENTAR':
                      return state + 1;
                    case 'DECREMENTAR':
                      return state - 1;
                    default:
                      return state; // Siempre retornar un estado por defecto
              }

-Dentro del componente llamamos al hook, que destructurado va a tener el state y dispatch que es quien va a llamar a la 
action de la funcion reductora.
-El hook tambien va a recibir dos argumentos. El primero es la funcionReductora y el segundo es el estado inicial. 
Se recomienda crear una variable que va contener el estado incial.

let estadoInicial = 'Algun Valor de cualquier tipo'
const [ state, dispatch ] = useReducer( funcionReductora, estadoInicial )

-Ya dentro del return suele llamarse el dispatch que es quien va a disparar la ejecucion de la accion que esta en la 
funcion reductora y ejecutara el codigo.

return (
      <button onClick={() => dispatch('Algunvalor')}>NombreDelBoton</button>
      
)

Ejemplo : 

        import { useReducer } from 'react';

        const funcionReductora = (state, action) => {
          switch (action) {
            case 'INCREMENTAR':
              return state + 1;
            case 'DECREMENTAR':
              return state - 1;
            default:
              return state;
          }
        };

        export default function Contador() {
          const estadoInicial = 0;
          const [state, dispatch] = useReducer(funcionReductora, estadoInicial);

          return (
            <div>
              <p>Contador: {state}</p>
              <button onClick={() => dispatch('INCREMENTAR')}>Incrementar</button>
              <button onClick={() => dispatch('DECREMENTAR')}>Decrementar</button>
            </div>
          );
        }


## useParams 
-Devuelve un objeto con los parametros que haya encontrado en la url   
useParams es un hook de React Router que se utiliza para acceder a los parámetros dinámicos de la URL en una aplicación React. 
Estos parámetros se definen en las rutas y permiten extraer valores específicos que forman parte del path.

-Dentro del componente rutas deberia colocar algo asi para definir la ruta que llevara parametros:
  <Route path ="/editar/:nombre/:id" element={<Editar/>} ></Route> Notar que hace uso de una / luego del nombre de componente
  seguido de :nombreParametro 

-El link tambien debe estar definido con los parametros correctos : 
   <Link to= {`editar/${contacto.nombre}/${contacto.id}`} </Link>
   o sin usar backticks: 
   <Link to={"editar/" + contacto.nombre + "/" + contacto.id}>Editar Usuario</Link>

-Y el componente que recibira y hara uso de los parametros debe importar el hook.
  import { useParams } from "react-router-dom" 

  const Editar = () => {

    const { nombre, id } = useParams();

    return (
      <div> Este es el {nombre}
            y este es el {id}
       </div> 

    )

  }
  Export default Editar

## Redux

## Formularios

-En formularios, en los input se debe reemplazar el for por htmlFor y en vez de id lleva name .

-Es util usar un useState cuyos parametros sean los name de los input.
[name,setName] = useState(''),
[tel,setTel] = useState(''),

-El form debe tener una escucha onSubmit y ejecutar la funcion correspondiente a ese evento. Se debe crear la funcion que 
maneje ese evento.

  <Form onSubmit={handleSubmit}>

- En los input en el value se le puede pasar como valor el estado para que se actualize en tiempo real.
  <input value={tel}>
  -Tambien deben tener el evento onChange para escuchar a medida que se van ingrersando datos y pueda ir actualizando su value.
  <input onChange={e => setTel(e.target.value)}>
     <form onSubmit={enviando}>
  Ejemplo:

  const [name, setName] = useState('')

  const [ciudad, setCiudad] = useState('')

const enviando = (e) => {
e.preventDefault()
console.log('Informacion enviada')
setName('')
setCiudad('')
}
return (

 <form onSubmit={enviando}>
        <input type="text" name="nombre" value={name} onChange={e => setName(e.target.value)} />    
        <input type="text" name="ciudad"  value={ciudad} onChange={e => setCiudad(e.target.value)} />
        <input type="submit" value="Enviar" />
  </form>
)

const [valor,setValor] = useState()

const sumas = (valor) => {
  console.log(valor + 5 )
  
}

const memo = useMemo( () => )

********************************
## Estilos 
-Una buena manera de usar estilos propios y evitar conflictos de clases a la hora de usar estilos generales, es usar modulos css . 
-Para hacerlo debo nombrar el archivo css con el sufijo module.
        estilos.module.css

-Luego en el componente que hara uso de ese estilo se debe importar colocandole un nombre a manera de identificarlo. (Notar que la importacion no lleva llaves {} )
  import miEstilo from '.ruta/del/archivo.css'

-En el elemento que hara uso de los estilos debo colocar el nombre que le asigne, entre llaves, mas el nombre que contiene el 
estilo.
  <div className= >  {miEstilo.container} </div>

-En caso de que la clase tenga guion ( - )  se debe colocar entre corchetes. 
  <div className= >  {miEstilo['card-container']} </div>

-En caso de tener que colocar mas de una clase se debe hacer siguiendo la anotacion de template strings.
  <div className= >  { ` ${miEstilo.card} ${miEstilo.container}` } </div>

  -En caso de necesitar usar clases separadas con giones, usar corchetes.
  <div className= >  { ` ${miEstilo[card-container] $(miEstilo[otro-estilo])} `} </div>



********************
## Datos Extras
-En un map luego de la funcion flecha se pueden usar () o {}. Pero hay unas diferencias
  
  iterable.map( (dato) => (Aqui el codigo jsx)) Aqui e return esta implicito

  iterable.map( (dato) => { return(Aqui el codigo jsx) }) Aqui se debe declarar el return
#### ¿cuando usar cada uno?
*** El uso de parentesis se puede dar cuando el jsx devuelto no es muy complejo.
*** El uso de llaves se puede usar cuando antes del return tengo que hacer alguna logica adicional. 
Como puede ser alguna validacion. Entonces hago la validacion, o lo que sea, y luego declaro el return() 
y alli coloco el jsx. 

-En caso de necesitar agregar eventos de escucha, hacerlo dentro de un useEffect y con una funcion nombrada 
y no con una funcion anonima, ya que es importante remover el evento al desmontar el componente y es mas
facil o menos trabajoso remover el evento con una funcion nombrada .
    funcion nombrada :
                      const handelEvent = () => { console.log('Click') }

  funcion anonima =   
                      window.addEventeListener('click', { codigo a ejecutar } )   
Para eliminar el evento lo que haria es :
             dentro del usseEfect en el return () => { windows.removeEventListener( 'click', handelEvent ) }                             
             