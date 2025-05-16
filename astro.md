-Para crear el proyecto:  npm cereate astro@latest
-Cuando se lanza el servidor de desarrolo , en el navegador aparece una barra de herramientas. Para quitarla ir a la consola dentro del proyecto y tipear npm run astro preferences disable devToolbar . Automaticamente se eliminara del navegador. En caso de necesitarlo nuevamente, el archivo qiue modifica esto está en la carpeta .astro/settings.json alli modificar o eliminar esta linea : 

                        "devToolbar": {
                                	"enabled": false
                                      }


-Dentro de la carpeta pages van a ir los archivos que seran cada una de las rutas del sitio. Cada archivo debe llevar la extension .astro

-Arriba del html hay una seccion hecha con 3 guiones --- --- Esta zona es en donde se puede colocar todo el codig   o js que se ejecutara antes de renderizar el archivo
