# Tablas de la Base de Datos 🛢️

A fecha de ***02 de abril de 2025***, se han definido las siguientes tablas para la base de datos. Estas tablas están actualmente pendientes de revisión por el tutor **Francisco Mera Calderón**.

## Índice

1. [Tablas](#tablas)
2. [Modificaciones](#modificaciones)

## Tablas

### Usuarios 👤

Esta tabla contiene la información básica de los usuarios registrados en la aplicación, como su nombre, apellidos, datos de contacto, y detalles adicionales como su puntuación y rol.

| Campo           | Tipo     | Longitud | Restricciones                                       | Null               |
|-----------------|----------|----------|-----------------------------------------------------|--------------------|
| idUsuario       | INT      | 6        | PK AUTOINCREMENTAL                                  | NOT NULL           |
| nombre          | VARCHAR  | 30       |                                                     | NOT NULL           |
| apellidos       | VARCHAR  | 40       |                                                     | NULL               |
| username        | VARCHAR  | 20       | UNIQUE                                              | NOT NULL           |
| email           | VARCHAR  | 30       | UNIQUE                                              | NOT NULL           |
| password        | VARCHAR  | 100      |                                                     | NOT NULL           |
| telefono        | VARCHAR  | 9        | UNIQUE                                              | NOT NULL           |
| fechaNacimiento | DATE     |          |                                                     | NOT NULL           |
| rol             | SET      |          | SET('ADMIN','ORGANIZADOR','COLABORADOR')           | DEFAULT 'COLABORADOR' |
| localidad       | VARCHAR  | 30       |                                                     | NOT NULL           |
| provincia       | VARCHAR  | 30       |                                                     | NOT NULL           |
| avatar          | VARCHAR  | 30       |                                                     | DEFAULT 'avatar.png' |
| puntuacionUser  | TINYINT  |          |                                                     | DEFAULT 0          |

---

### Eventos 🎉

Esta tabla almacena los eventos creados por los usuarios, incluyendo detalles como las fechas de inicio y fin, la descripción del evento, su estado y el modo (comunitario o competitivo).

| Campo         | Tipo     | Longitud | Restricciones                                                      | Null                |
|---------------|----------|----------|--------------------------------------------------------------------|---------------------|
| idEvento      | INT      | 6        | PK AUTOINCREMENTAL                                                 | NOT NULL            |
| titulo        | VARCHAR  | 40       |                                                                    | NOT NULL            |
| descripcion   | VARCHAR  | 100      |                                                                    | NOT NULL            |
| fechaCreacion | DATE     |          |                                                                    | NOT NULL            |
| fechaInicio   | DATE     |          |                                                                    | NOT NULL            |
| fechaFin      | DATE     |          |                                                                    | NOT NULL            |
| idUsuario     | INT      | 6        | FK → usuarios(idUsuario)                                           | NOT NULL            |
| direccion     | VARCHAR  | 40       |                                                                    | NOT NULL            |
| localidad     | VARCHAR  | 30       |                                                                    | NOT NULL            |
| provincia     | VARCHAR  | 30       |                                                                    | NOT NULL            |
| idCategoria   | INT      | 6        | FK → categorias(idCategoria)                                       | NOT NULL            |
| modoEvento    | SET      |          | SET('Comunitario','Competitivo')                                  | DEFAULT 'Comunitario' |
| estado        | SET      |          | SET('Por Empezar','En Curso','Finalizado','Cancelado')            | DEFAULT 'Por Empezar' |

---

### Categorías 🗂️

La tabla de categorías se utiliza para organizar los **eventos** en diferentes categorías, como pueden ser videojuegos, juegos de mesa, deportes, música, etc.

| Campo        | Tipo     | Longitud | Restricciones            | Null     |
|--------------|----------|----------|--------------------------|----------|
| idCategoria  | INT      | 6        | PK AUTOINCREMENTAL       | NOT NULL |
| nombre       | VARCHAR  | 30       | UNIQUE                   | NOT NULL |

---

### UsuarioEventos 🔗

Esta tabla intermedia representa la relación **muchos a muchos** entre los usuarios y los eventos a los que se unen.

| Campo      | Tipo     | Longitud | Restricciones              | Null     |
|------------|----------|----------|----------------------------|----------|
| idUsuario  | INT      | 6        | PK, FK → usuarios(idUsuario) | NOT NULL |
| idEvento   | INT      | 6        | PK, FK → eventos(idEvento)   | NOT NULL |


---
## Modificaciones

**Modificaci&oacute;n** - ***(07/02/2025)***
- Se ha eliminado el campo **Organizador** de la tabla **Usuarios**.
- Ahora **Organizador** forma parte de `Rol` en la tabla **Usuarios**.
- El campo **Nombre** de la tabla **Categor&iacute;s** ha pasado a ser `UNIQUE` para evitar creaciones duplicadas.
- Se ha a&ntilde;adido un estado m&aacute;s al campo `Estado` de la tabla **Eventos** el nuevo estado es `Cancelado`.

**Modificaci&oacute;n** - ***(10/02/2025)***
1. **Usuarios:**
   - **Cambio en el tipo de dato de `idUsuario`**: Se cambió de `TINYINT` a `INT` para adaptarse a un rango de valores más grande.
   - **Ajuste en el campo `rol`**: Se agregó un valor por defecto `'COLABORADOR'` al campo `rol` usando `DEFAULT 'COLABORADOR'`.
   - **Adición de campo `puntuacionUser`**: Se añadió un nuevo campo `puntuacionUser` de tipo `TINYINT` con valor por defecto `0`.

2. **Eventos:**
   - **Cambio en el tipo de dato de `idEvento`**: Se cambió de `TINYINT` a `INT` para un rango de valores más amplio.
   - **Cambio en el tipo de dato de `idCategoria`**: Se cambió de `VARCHAR(6)` a `INT(6)` que estaba erróneamente configurado.
   - **Ajuste en el campo `modoEvento`**: Se cambió el tipo de dato a `SET('Comunitario', 'Competitivo')` y se añadió el valor por defecto `'Comunitario'`.
   - **Ajuste en el campo `estado`**: Se cambió el tipo de dato a `SET('Por Empezar', 'En Curso', 'Finalizado', 'Cancelado')` y se añadió el valor por defecto `'Por Empezar'`.

3. **Categorías:**
   - **Cambio en el tipo de dato de `idCategoria`**: Se cambió de `TINYINT` a `INT` para un rango de valores más grande.

4. **UsuarioEventos:**
   - **Creación de la tabla `usuarioeventos`**: Se añadió la nueva tabla intermedia para representar la relación muchos a muchos entre usuarios y eventos.
   - **Definición de claves foráneas**: Se añadieron claves foráneas a los campos `idUsuario` e `idEvento` para hacer referencia a las tablas `usuarios` y `eventos`, respectivamente.
   - **Combinación de claves primarias**: La tabla tiene como clave primaria la combinación de los campos `idUsuario` e `idEvento`.
