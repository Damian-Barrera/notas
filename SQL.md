CREATE DATABASE nombre_de_base_de_datos;

USE nombre_de_base_de_datos;

CREATE TABLE nombre_tabla (id INT AUTO_INCREMENT PRIMARY KEY, nombre VARCHAR(50), email VARCHAR(100));

INSERT INTO nombre_tabla (nombre, email) VALUES ('Juan', 'juan@mail.com');  

SELECT * FROM nombre_tabla;

SELECT nombre FROM nombre_tabla WHERE id = 1;
SELECT nombre, apellido FROM nombre_tabla WHERE campo >= 2 AND campo <= 5; // Ejemplo para usar el AND   

UPDATE nombre_tabla SET email = 'nuevo@mail.com' WHERE id = 1;

DELETE FROM nombre_tabla WHERE id = 1;

DROP TABLE nombre_tabla;

DROP DATABASE nombre_de_base_de_datos;

//Borra todos los datos de la tabla y reinicia el AUTO_INCREMENT a 1, sin borrar la estructura de la tabla.
TRUNCATE TABLE nombre_tabla;

-- Eliminar una columna
ALTER TABLE nombre_tabla DROP COLUMN password;

// Para agregar una columna a una tabla existente.
ALTER TABLE nombre_tabla ADD COLUMN nombre_columna VARCHAR(255); 
// Para agregar la columna en una posicion especifica
ALTER TABLE nombre_tabla ADD COLUMN nombre_columna VARCHAR(255) AFTER nombre_columna; 
