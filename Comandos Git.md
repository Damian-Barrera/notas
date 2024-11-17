## Configuracio de Git

git config --global user.name "usuario"
git config --global user.email "usuario@dominio.com"

git config --global --list : Para ver la informacion del usuario

## Para agregar a repositorio remoto

-git remote add url-del-repositorio-remoto
-luego el git push origin master


## Clonar Repositorio

git clone 'https://ruta-del-repositorio'

Sino tambien se puede hacer a travez de SSH previamente habiendo creada una KEY publica. 
   git clone 'git@github.com:usuario/proyecto'

-git push origin master : Para agregar a repositorio de Github.
