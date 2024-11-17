## Iterar Objetos

-Iterar claves de objetos se puede usar Object.keys(nombreDelObjeto)
-Iterar valores de objetos se puede usar Object.values(nombredelobjeto)
-Iterar ambos clave/valor de objetos Object.entries(nombreDelObjeto)

            const nombres = {
                    jessica: 31,
                    caro: 29,
                    azul: 37,
                    anto: 28,
                    flor:24,
                    vero: 34
                }

  Object.keys(nombres).map(name => {console.log(name)})   \\ jessica,caro,azul,anto,flor,vero
  Object.values(nombres).map(name => {console.log(name)})  \\ 31,29,,37,28,24,34
  Object.entries(nombres).map(name => {console.log(name)}) \\[jessica,31],[caro,29],[azul,37],[anto,28]