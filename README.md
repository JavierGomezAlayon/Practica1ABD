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

	Además le di permisos de administrador al usuario admin_biblio
	<img width="959" height="50" alt="image" src="https://github.com/user-attachments/assets/d40c916a-ecc8-4f3d-aca4-bdc4b8b59fc2" />

	
3. Crear un rol llamado lectores con permisos únicamente de consulta sobre todas las tablas de la base de datos.

	- Comando
	```postgreSQL
 	create role lectores;
 	grant connect on database biblioteca to lectores;
 	grant usage on schema public to lectores;
    alter default privileges in schema public grant select on tables to lectores;
	```
	- Respuesta


	<img width="151" height="26" alt="image" src="https://github.com/user-attachments/assets/e3650ba8-2862-4a4e-96eb-019ecb666e7e" />.
 
 	<img width="65" height="20" alt="image" src="https://github.com/user-attachments/assets/1f62810d-4e57-4032-844e-24cec0e02e3c" />.

  
 	<img width="317" height="23" alt="image" src="https://github.com/user-attachments/assets/6857049b-f904-4dea-b7fe-8829e8c94584" />



	Primero creo el rol. Garantizo que puedan conectarse, que puedan usar el esquema public y que puedan leer todas las tablas que se creen en el esquema.
	
4. Asignar el usuario usuario_biblio a este rol.

	- Comando
	```
 	grant lectores to usuario_biblio;
	```
	- Respuesta
	<img width="141" height="27" alt="image" src="https://github.com/user-attachments/assets/12330dc5-2937-4b7f-b9ed-3e24501dabc6" />

 
5. Consultar las tablas del sistema para listar todos los usuarios creados (pg_roles).

	- Comando
	```
 	select * from pg_roles;
	```
	- Respuesta
 	<img width="1279" height="532" alt="image" src="https://github.com/user-attachments/assets/10adf829-234d-4223-a2b1-5f2ee9277c02" />

6. Cambiar la contraseña del usuario usuario_biblio.

	- Comando
	```
 	alter user usuario_biblio with password '123';
	```
	- Respuesta
	<img width="142" height="24" alt="image" src="https://github.com/user-attachments/assets/e5a1b36c-f3fb-4f43-81a9-110e9a399197" />

 
7. Configurar permisos de tal forma que el usuario usuario_biblio no pueda eliminar registros en ninguna tabla.

	- Comando
	```
 	alter default privileges in schema public revoke delete on tables from usuario_biblio;
	```
	- Respuesta
 	<img width="330" height="23" alt="image" src="https://github.com/user-attachments/assets/a1cde256-cacc-4de8-a756-4fab85a80dbf" />
	Esto lo que hará es que en las tablas que cree(todavía no he creado ninguna) se ponga de forma por defecto que usuario_biblio no pueda realizar la operación delete en ellas.
    
## Creación de tablas
1. Crear las siguientes tablas con sus respectivas claves primarias:

	1. autores(id_autor, nombre, nacionalidad)
	2. libros(id_libro, titulo, año_publicacion, id_autor)
	3. prestamos(id_prestamo, id_libro, fecha_prestamo, fecha_devolucion, usuario_prestatario)

	- Comando
	```SQL
 	create table autores(
		id_autor serial primary key,
		nombre varchar(100) not null,
		nacionalidad varchar(60)
	);
	```
 	```SQL
 	create table libros(
		id_libro serial primary key,
		titulo varchar(100) not null,
  		año_publicacion integer,
  		id_autor integer not null,
  		constraint fk_autor
  			foreign key (id_autor) references autores (id_autor) on delete cascade
	);
	```
  	```SQL
 	create table prestamos (
    id_prestamo serial primary key,
    id_libro integer not null,
    fecha_prestamo date not null,
    fecha_devolucion date,
    usuario_prestatario varchar(100) not null,
    constraint fk_libro
        foreign key (id_libro) references libros (id_libro) on delete cascade
	);
	```
	- Respuesta (fue la misma respuesta para los tres)
	<img width="167" height="20" alt="image" src="https://github.com/user-attachments/assets/63214c7a-1669-4e78-abf2-37f0ee98bf7b" />

2. Establecer las claves foráneas correspondientes.
	Ya se hizo en el comando anterior

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
 
