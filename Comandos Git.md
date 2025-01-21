## Configuracio de Git

git config --global user.name "usuario"
git config --global user.email "usuario@dominio.com"

git config --global --list : Para ver la informacion del usuario

## Para agregar a repositorio remoto

-git remote add origin url-del-repositorio-remoto
-git push -u origin master

-git rm --cached nombre_de_archivo : Sirve para eliminar un archivo que estaba siendo seguido por git. Si coloco un archivo en el gitignore dejara de rastrearlo pero si antes lo habia rastreado y agregado , seguira existiendo. Con este comando lo quitara tambien del arbol. 


## Clonar Repositorio

git clone 'https://ruta-del-repositorio'

Sino tambien se puede hacer a travez de SSH previamente habiendo creada una KEY publica. 
   git clone 'git@github.com:usuario/proyecto'

-git push origin master : Para agregar a repositorio de Github.
