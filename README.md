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
    Después me di cuenta de que necesitaba una condición extra para que la fecha de devolución no fuera anterior a la fecha de prestamo:
   ```sql
   alter table prestamos
	add constraint chk_fechas
	check (fecha_devolucion is null or fecha_devolucion >= fecha_prestamo);
   ```
	- Respuesta (fue la misma respuesta para los tres)
	<img width="167" height="20" alt="image" src="https://github.com/user-attachments/assets/63214c7a-1669-4e78-abf2-37f0ee98bf7b" />

 

3. Establecer las claves foráneas correspondientes.
	Ya se hizo en el comando anterior

## Inserción de datos
1. Insertar al menos 5 autores, 8 libros y 5 préstamos de ejemplo.
	- Comando
	```SQL
 	insert into autores (nombre, nacionalidad) values
		('Miguel de Cervantes', 'Española'),
		('Gabriel García Márquez', 'Colombiana'),
		('Isabel Allende', 'Chilena'),
		('Federico García Lorca', 'Española'),
		('Jane Austen', 'Británica'),
		('Joanne Rowling','Británica');
	```
  	```sql
 	insert into libros (titulo, año_publicacion, id_autor) values
		('Don Quijote de la Mancha', 1605, 1),
		('Novelas ejemplares', 1613, 1),
		('Cien años de soledad', 1967, 2),
		('El amor en los tiempos del cólera', 1985, 2),
		('La casa de los espíritus', 1982, 3),
		('Romancero gitano', 1928, 4),
		('Orgullo y prejuicio', 1813, 5),
		('Harry Potter y la piedra filosofal', 1997, 6);
   	```
   	```sql
 	insert into prestamos (id_libro, fecha_prestamo, fecha_devolucion, usuario_prestatario) values
		(1, '2025-09-01', '2025-09-15', 'usuario1'),
		(3, '2025-09-05', null, 'usuario2'),
		(5, '2025-09-07', '2025-09-14', 'usuario3'),
		(6, '2025-09-10', null, 'usuario4'),
		(8, '2025-09-12', '2025-09-19', 'usuario5');
   	```
	- Respuesta
	<img width="146" height="23" alt="image" src="https://github.com/user-attachments/assets/3af9132e-ff96-4cf2-9d86-3cbfa0b812dc" />
	<img width="142" height="29" alt="image" src="https://github.com/user-attachments/assets/f260e678-75e9-4c8c-ae53-5533ad656082" />
	<img width="145" height="23" alt="image" src="https://github.com/user-attachments/assets/a68d96e1-789e-47db-96d8-371caa5c9650" />

 
## Consultas básicas
1. Listar todos los libros con su autor correspondiente.

	- Comando
	```
 	select titulo,nombre as autor
	from libros
	natural join autores;
	```
	- Respuesta
	<img width="813" height="279" alt="image" src="https://github.com/user-attachments/assets/1a92a351-aa69-4bf7-ac23-f00b9ccb0d7e" />

 
2. Mostrar los préstamos que aún no tienen fecha de devolución.

	- Comando
	```
 	select *
	from prestamos
	where fecha_devolucion is null;
	```
	- Respuesta
	<img width="1089" height="138" alt="image" src="https://github.com/user-attachments/assets/eb14dbd6-f9e8-4e7c-b749-025febbe20a7" />
 
3. Obtener los autores que tienen más de un libro registrado.

	- Comando
	```
 	select nombre
	from autores
	where id_autor in (
	    select id_autor
	    from libros
	    group by id_autor
	    having count(*) > 1
	);
	```
	- Respuesta
 	<img width="352" height="140" alt="image" src="https://github.com/user-attachments/assets/bcf803dd-e9fb-4358-9b61-dbb4e6070248" />


## Consultas con agregación
1. Calcular el número total de préstamos realizados.

	- Comando
	```
 	select count(*)
	from prestamos;
	```
	- Respuesta
	<img width="111" height="104" alt="image" src="https://github.com/user-attachments/assets/04df909a-588f-4310-9d82-fb9e4104ee0c" />

2. Obtener el número de libros prestados por cada usuario.

	- Comando
	```
 	select count(*)
	from prestamos
 	group by usuario_prestatario;
	```
	- Respuesta
 	<img width="117" height="206" alt="image" src="https://github.com/user-attachments/assets/1a8842c0-ad6f-46ce-bc33-997227ee3fe4" />


## Modificación de datos
1. Actualizar la fecha de devolución de un préstamo pendiente.

	- Comando
	```
 	update prestamos
	set fecha_devolucion = '2025-09-20'
	where id_prestamo = 4;
	```
	- Respuesta
 
2. Eliminar un libro y comprobar el efecto en la tabla de préstamos (usar ON DELETE CASCADE o justificar el comportamiento).

	- Comando
	```
 	delete from libros
	where id_libro=1;
	select * from prestamos;
	```
	- Respuesta
 	<img width="1085" height="181" alt="image" src="https://github.com/user-attachments/assets/484dc7fc-87b2-406d-a9b8-73470bb095dd" />

## Creación de vistas
1. Crear una vista llamada vista_libros_prestados que muestre: título del libro, autor y nombre del prestatario.

	- Comando
	```
 	create view vista_libros_prestados
	as select titulo, nombre as autor, usuario_prestatario
		from prestamos natural join libros natural join autores;
	```
	- Respuesta
	<img width="153" height="29" alt="image" src="https://github.com/user-attachments/assets/1e893cd2-dcf1-4774-b804-22a8b3ea2ca1" />

 
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
 
