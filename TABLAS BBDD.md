
## Tablas de la Base de Datos 🛢️

A fecha de ***02 de abril de 2025***, se han definido las siguientes tablas para la base de datos. Estas tablas están actualmente pendientes de revisión por el tutor **Francisco Mera Calderón**.

---
### Usuarios 👤

Esta tabla contiene la información básica de los usuarios registrados en la aplicación, como su nombre, apellidos, datos de contacto, y detalles adicionales como su puntuación y rol.

| Campo          | Tipo      | Longitud | Restricciones            | Null               |
|----------------|-----------|----------|--------------------------|--------------------|
| IdUsuario      | TINYINT   | 6        | PK AUTOINCREMENTAL        | NOT                |
| Nombre         | VARCHAR   | 30       |                          | NOT                |
| Apellidos      | VARCHAR   | 40       |                          | NULL                   |
| Username       | VARCHAR   | 20       | UNIQUE                    | NOT                |
| Email          | VARCHAR   | 30       | UNIQUE                    | NOT                |
| Password       | VARCHAR   | 100      |                          | NOT                |
| Telefono       | INT       | 9        | UNIQUE                    | NOT                |
| FechaNacimiento| DATE      |          |                          | NOT                |
| Rol            | SET       |          | SET('ADMIN', 'USER')      | Default 'USER'     |
| Localidad      | VARCHAR   | 30       |                          | NOT                |
| Provincia      | VARCHAR   | 30       |                          | NOT                |
| Avatar         | VARCHAR   | 30       | Default 'png'             | Default 'png'      |
| PuntuacionUser | TINYINT   |          |                          | Default 0          |
| Organizador    | BOOLEAN   | 1        |                          | Default 'F'        |

---

### Eventos 🎉

Esta tabla almacena los eventos creados por los usuarios, incluyendo detalles como las fechas de inicio y fin, la descripción del evento, su estado, y el modo (comunitario o competitivo).

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
| Estado       | SET       |          | SET('Por Empezar','En Curso','Finalizado')             | Default 'Por Empezar' |

---

### Categorías 🗂️

La tabla de categorías se utiliza para organizar los **eventos** en diferentes categorías, como pueden ser videojuegos, juegos de mesa, deportes, música, etc.

| Campo        | Tipo      | Longitud | Restricciones            | Null               |
|--------------|-----------|----------|--------------------------|--------------------|
| IdCategoria  | TINYINT   | 6        | PK AUTOINCREMENTAL        | NOT                |
| Nombre       | VARCHAR   | 30       |                          | NOT                |
