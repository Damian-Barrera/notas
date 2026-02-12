## Para empezar a usar EJS se debe instalar\_

npm i ejs

-El archivo en donde se usaran los datos se deben llamar con la extension ejs : mi_archivo.ejs
-ES importante que los archivos esten dentro de la carpeta views. Es una convencion porque cuando expres intente renderizar
´res.render("index", { usuarios: rows });´ automaticamente intentara buscar en views/usuarios.ejs

-Luego de crear el app, en la siguiente linea colocar:

    ```
     app.set("view engine", "ejs");

    ```

-Para imprimir en pantalla (mostrar datos) : <%= %> :
Esto se usa cuando se quiere mostrar una variable en HTML.
``` <p>Total de usuarios: <%= datos.length %></p> ```

-EJECUTAR JavaScript (sin mostrarlo) <% %> :
Esto no imprime nada, solo ejecuta código.
``` <% datos.forEach(usuario => { %> ```

-Para usar estilos css:
Los archivos css deben estar en la carpeta public si o si . y dentro del index.js del backend debe estar declarado asi

``` app.use(express.static("public")); ```

-Para poder reutilizar codigo de otros documentos se hace de la siguiente manera:

```
<%- include('nombre_del_archivo') %>
<%- include('footer.ejs') %>

```
-Insertar fragmentos condicionalmente (ternarios)

```<p>
  <%= usuario.edad >= 18 ? "Mayor de edad" : "Menor de edad" %>
</p>
```
