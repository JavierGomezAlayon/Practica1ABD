# Practica1ABD
En esta práctica voy a ver lo básico de postgreSQL, al crear una pequeña base de datos de prueba con el lenguaje mencionado

1. Creación de la base de datos
    1. Crear una base de datos llamada biblioteca.
	
2. Creación de usuarios
    1. Crear dos usuarios:
	    1. admin_biblio con permisos de administrador sobre la base de datos.
	    2. usuario_biblio con permisos solo de lectura.
    2. Crear un rol llamado lectores con permisos únicamente de consulta sobre todas las tablas de la base de datos.
    3. Asignar el usuario usuario_biblio a este rol.
    4. Consultar las tablas del sistema para listar todos los usuarios creados (pg_roles).
    5. Cambiar la contraseña del usuario usuario_biblio.
    6. Configurar permisos de tal forma que el usuario usuario_biblio no pueda eliminar registros en ninguna tabla.
    
3. Creación de tablas
    1. Crear las siguientes tablas con sus respectivas claves primarias:
	    1. autores(id_autor, nombre, nacionalidad)
	    2. libros(id_libro, titulo, año_publicacion, id_autor)
	    3. prestamos(id_prestamo, id_libro, fecha_prestamo, fecha_devolucion, usuario_prestatario)
    2. Establecer las claves foráneas correspondientes.
    
4. Inserción de datos
    1. Insertar al menos 5 autores, 8 libros y 5 préstamos de ejemplo.
    
5. Consultas básicas
    1. Listar todos los libros con su autor correspondiente.
    2. Mostrar los préstamos que aún no tienen fecha de devolución.
    3. Obtener los autores que tienen más de un libro registrado.
    
6. Consultas con agregación
    1. Calcular el número total de préstamos realizados.
    2. Obtener el número de libros prestados por cada usuario.
    
7. Modificación de datos
    1. Actualizar la fecha de devolución de un préstamo pendiente.
    2. Eliminar un libro y comprobar el efecto en la tabla de préstamos (usar ON DELETE CASCADE o justificar el comportamiento).
    
8. Creación de vistas
    1. Crear una vista llamada vista_libros_prestados que muestre: título del libro, autor y nombre del prestatario.
    2. Conceder permisos de consulta sobre esta vista únicamente a usuario_biblio.
    
9. Funciones y consultas avanzadas
    1. Crear una función que reciba el nombre de un autor y devuelva todos los libros escritos por él.
    2. Crear una consulta que devuelva los tres libros más prestados.
    
10. Exportación e importación de datos
    1. Exportar el contenido de la tabla libros a un archivo CSV.
    2. Importar datos adicionales de autores desde un archivo CSV externo.
    
