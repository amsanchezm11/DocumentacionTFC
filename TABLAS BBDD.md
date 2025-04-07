# Tablas de la Base de Datos 🛢️

A fecha de ***02 de abril de 2025***, se han definido las siguientes tablas para la base de datos. Estas tablas están actualmente pendientes de revisión por el tutor **Francisco Mera Calderón**.

## Índice

1. [Tablas](#tablas)
2. [Modificaciones](#modificaciones)

## Tablas

### Usuarios 👤

Esta tabla contiene la información básica de los usuarios registrados en la aplicación, como su nombre, apellidos, datos de contacto, y detalles adicionales como su puntuación y rol.

| Campo          | Tipo      | Longitud | Restricciones            | Null               |
|----------------|-----------|----------|--------------------------|--------------------|
| IdUsuario      | TINYINT   | 6        | PK AUTOINCREMENTAL       | NOT                |
| Nombre         | VARCHAR   | 30       |                          | NOT                |
| Apellidos      | VARCHAR   | 40       |                          | NULL               |
| Username       | VARCHAR   | 20       | UNIQUE                   | NOT                |
| Email          | VARCHAR   | 30       | UNIQUE                   | NOT                |
| Password       | VARCHAR   | 100      |                          | NOT                |
| Telefono       | INT       | 9        | UNIQUE                   | NOT                |
| FechaNacimiento| DATE      |          |                          | NOT                |
| Rol            | SET       |          | SET('ADMIN','ORGANIZADOR' 'COLABORADOR')      | Default 'COLABORADOR'     |
| Localidad      | VARCHAR   | 30       |                          | NOT                |
| Provincia      | VARCHAR   | 30       |                          | NOT                |
| Avatar         | VARCHAR   | 30       | Default 'png'             | Default 'png'     |
| PuntuacionUser | TINYINT   |          |                          | Default 0          |

---

### Eventos 🎉

Esta tabla almacena los eventos creados por los usuarios, incluyendo detalles como las fechas de inicio y fin, la descripción del evento, su estado y el modo (comunitario o competitivo).

| Campo        | Tipo      | Longitud | Restricciones                                          | Null              |
|--------------|-----------|----------|--------------------------------------------------------|-------------------|
| IdEvento     | TINYINT   | 6        | PK AUTOINCREMENTAL                                     | NOT               |
| Titulo       | VARCHAR   | 40       |                                                        | NOT               |
| Descripcion  | VARCHAR   | 100      |                                                        | NOT               |
| FechaCreacion| DATE      |          |                                                        | NOT               |
| FechaInicio  | DATE      |          |                                                        | NOT               |
| FechaFin     | DATE      |          |                                                        | NOT               |
| IdUsuario    | TINYINT   | 6        | FK                                                     | NOT               |
| Direccion    | VARCHAR   | 40       |                                                        | NOT               |
| Localidad    | VARCHAR   | 30       |                                                        | NOT               |
| Provincia    | VARCHAR   | 30       |                                                        | NOT               |
| IdCategoria  | VARCHAR   | 6        | FK                                                     | NOT               |
| ModoEvento   | SET       |          | SET('Comunitario','Competitivo')                       | Default 'Comunitario' |
| Estado       | SET       |          | SET('Por Empezar','En Curso','Finalizado', 'Cancelado')             | Default 'Por Empezar' |

---

### Categorías 🗂️

La tabla de categorías se utiliza para organizar los **eventos** en diferentes categorías, como pueden ser videojuegos, juegos de mesa, deportes, música, etc.

| Campo        | Tipo      | Longitud | Restricciones            | Null               |
|--------------|-----------|----------|--------------------------|--------------------|
| IdCategoria  | TINYINT   | 6        | PK AUTOINCREMENTAL       | NOT                |
| Nombre       | VARCHAR   | 30       | UNIQUE                   | NOT                |

---
## Modificaciones

**Modificaci&oacute;n** - ***(07/02/2025)***
- Se ha eliminado el campo **Organizador** de la tabla **Usuarios**.
- Ahora **Organizador** forma parte de **Rol** en la tabla **Usuarios**.
- El campo **Nombre** de la tabla **Categor&iacute;s** ha pasado a ser **UNIQUE** para evitar creaciones duplicadas.
- Se ha a&ntilde;adido un estado m&aacute;s al campo **Estado** de la tabla **Eventos** el nuevo estado es ***Cancelado***.

