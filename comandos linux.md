-sudo su : Para ser usuario root
-apt update :  Para actualizar repositorios (creo que es para los programas ).
-apt upgrade : Para actualizar tambien( creo que es para el sistema ).
-apt autoremove : Elimina dependencias o archivos obsoletos.
-sudo sh -c "echo 3 > /proc/sys/vm/drop_caches" : Este comando es para vaciar cahce luego de usar algun programa pesado y que haya quedado lento.
-sudo systemctl restart display-manager : Reinicia el entorno grafico. (sin reiniciar el SO)





*********************
-Para personalizar mint: 
  Buscar en el navegador cinnamon look (cinamon porque es el escritorio que usa mint. Existe Gnome,Kde, xfce, etc). Elegir un pack de iconos. 
Se debe de crear una carpeta dentro de la carpeta personal (vendria a ser /home/usuario) donde dice usuario, va a tener el nomnbre propio que se le haya puesto. Enrtar ahi, clic derecho y mostrar archivos ocultos. Se va a necesitar la carpeta .themes y .icons (si no estan, crearlas). Ver el archivo que se descargo, abrirlo, buscar extraer y elegir la carpeta de iconos. 
Ir al boton inicio, temas,iconos y buscar el que se haya descargado y solo seleccionarlo y esperar a que cambien. Ver que tambien se puede cambiar el cursor, los temas .

-Para instalar otro gestor de software (para buscar y descargar programas). 
Existe el gestor snapd, muy usado en ubuntu, pero que en mint esta como bloqueado. Para poder instalarlo primero se debe eliminar la restriccion: sudo rm /etc/apt/preferences.d/nosnap.pref
Ahora si, a instalar con : sudo apt install snapd.
Esto es util para poder tener un abanico mas amplio a la hora de instalar alguna aplicacion.
Se puede visitar la web snapcraft.io para ver las aplicaiones disponibles. 

-flatpack es otro gestor de paquetes. se puede usar el flatpak --help para probar que si esta instalado. 
Para ver las aplicaciones disponibles ir a la web flathub.org . 
 Ejempo: Para instalar telegram. flatpak install telegram (seguir las opciones que me van diciendo)
    Si queiero desinstalar, flatpak remove telegram . Suelen quedar residuos inutilizables de las aplicaciones eliminadas. Para ello escribo :flatpak unistall --unused  
