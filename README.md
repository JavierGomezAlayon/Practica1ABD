# Practica1ABD
En esta práctica voy a ver lo básico de postgreSQL, al crear una pequeña base de datos de prueba con el lenguaje mencionado

## Creación de la base de datos
1. Crear una base de datos llamada biblioteca.
	- Comando
	```
	create database biblioteca;
	```
	- Respuesta
	<img width="199" height="22" alt="image" src="https://github.com/user-attachments/assets/96c5f6fc-afbc-47ea-9306-c8e33d7ea4db" />

	
## Creación de usuarios
1. Crear dos usuarios:
	- Comando
	```
 	CREATE USER admin_biblio WITH PASSWORD '123';
	CREATE USER usuario_biblio WITH PASSWORD '123';
	```
	- Respuesta (misma respuesta para ambos comandos)
	<img width="154" height="21" alt="image" src="https://github.com/user-attachments/assets/4c1baa81-fd70-4209-bbbc-a66c3754af69" />

2. Crear un rol llamado lectores con permisos únicamente de consulta sobre todas las tablas de la base de datos.
	- Comando
	```
 
	```
	- Respuesta
 
3. Asignar el usuario usuario_biblio a este rol.

	- Comando
	```
 
	```
	- Respuesta
 
4. Consultar las tablas del sistema para listar todos los usuarios creados (pg_roles).

	- Comando
	```
 
	```
	- Respuesta
 
5. Cambiar la contraseña del usuario usuario_biblio.

	- Comando
	```
 
	```
	- Respuesta
 
6. Configurar permisos de tal forma que el usuario usuario_biblio no pueda eliminar registros en ninguna tabla.

	- Comando
	```
 
	```
	- Respuesta
 
    
## Creación de tablas
1. Crear las siguientes tablas con sus respectivas claves primarias:
	1. autores(id_autor, nombre, nacionalidad)
	2. libros(id_libro, titulo, año_publicacion, id_autor)
	3. prestamos(id_prestamo, id_libro, fecha_prestamo, fecha_devolucion, usuario_prestatario)
2. Establecer las claves foráneas correspondientes.

	- Comando
	```
 
	```
	- Respuesta
 

## Inserción de datos
1. Insertar al menos 5 autores, 8 libros y 5 préstamos de ejemplo.
	- Comando
	```
 
	```
	- Respuesta
 
## Consultas básicas
1. Listar todos los libros con su autor correspondiente.

	- Comando
	```
 
	```
	- Respuesta
 
2. Mostrar los préstamos que aún no tienen fecha de devolución.

	- Comando
	```
 
	```
	- Respuesta
 
3. Obtener los autores que tienen más de un libro registrado.

	- Comando
	```
 
	```
	- Respuesta
 

## Consultas con agregación
1. Calcular el número total de préstamos realizados.

	- Comando
	```
 
	```
	- Respuesta
 
2. Obtener el número de libros prestados por cada usuario.

	- Comando
	```
 
	```
	- Respuesta
 

## Modificación de datos
1. Actualizar la fecha de devolución de un préstamo pendiente.

	- Comando
	```
 
	```
	- Respuesta
 
2. Eliminar un libro y comprobar el efecto en la tabla de préstamos (usar ON DELETE CASCADE o justificar el comportamiento).

	- Comando
	```
 
	```
	- Respuesta
 
## Creación de vistas
1. Crear una vista llamada vista_libros_prestados que muestre: título del libro, autor y nombre del prestatario.

	- Comando
	```
 
	```
	- Respuesta
 
2. Conceder permisos de consulta sobre esta vista únicamente a usuario_biblio.

	- Comando
	```
 
	```
	- Respuesta
 
## Funciones y consultas avanzadas
1. Crear una función que reciba el nombre de un autor y devuelva todos los libros escritos por él.

	- Comando
	```
 
	```
	- Respuesta
 
2. Crear una consulta que devuelva los tres libros más prestados.

	- Comando
	```
 
	```
	- Respuesta
 
## Exportación e importación de datos
1. Exportar el contenido de la tabla libros a un archivo CSV.

	- Comando
	```
 
	```
	- Respuesta
 
2. Importar datos adicionales de autores desde un archivo CSV externo.
    
	- Comando
	```
 
	```
	- Respuesta
 
