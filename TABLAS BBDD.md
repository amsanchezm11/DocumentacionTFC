# Tablas de la Base de Datos 🛢️

> [!NOTE]
> A fecha de ***29 de mayo de 2025***, se han definido las siguientes tablas para la base de datos. Estas tablas han sido revisadas junto al tutor **Francisco Mera Calderón**.

## Índice

1. [Tablas](#tablas)
2. [Modificaciones](#modificaciones)

## Tablas

### Usuarios 👤

Esta tabla contiene la información básica de los usuarios registrados en la aplicación, como su nombre, apellidos, datos de contacto, y detalles adicionales como su sexo y rol.

| Campo           | Tipo    | Longitud | Restricciones                | Null     |
| --------------- | ------- | -------- | ---------------------------- | -------- |
| IdUsuario       | INT     | 11       | PK AUTOINCREMENTAL           | NOT NULL |
| Nombre          | VARCHAR | 30       |                              | NOT NULL |
| Apellidos       | VARCHAR | 40       |                              | NOT NULL |
| Username        | VARCHAR | 20       | UNIQUE                       | NOT NULL |
| Email           | VARCHAR | 60       | UNIQUE                       | NOT NULL |
| Password        | VARCHAR | 100      |                              | NOT NULL |
| Telefono        | VARCHAR | 9        | UNIQUE                       | NOT NULL |
| FechaNacimiento | DATE    |          |                              | NOT NULL |
| Rol             | VARCHAR | 11       |                              | NOT NULL |
| Sexo            | VARCHAR | 6        |                              | NOT NULL |
| Localidad       | VARCHAR | 50       |                              | NOT NULL |
| IdProvincia     | INT     |          | FK → provincias(IdProvincia) | NOT NULL |
| FechaCreacion   | DATE    |          |                              | NOT NULL |
| Avatar          | VARCHAR | 30       | DEFAULT 'avatar.svg'         | NOT NULL |

---

### Eventos 🎉

Esta tabla almacena los eventos creados por los usuarios, incluyendo detalles como las fechas de inicio y fin, la descripción del evento, su estado y el modo (comunitario o competitivo).

| Campo            | Tipo    | Longitud | Restricciones                      | Null     |
| ---------------- | ------- | -------- | ---------------------------------- | -------- |
| IdEvento         | INT     |          | PK AUTOINCREMENTAL                 | NOT NULL |
| Titulo           | VARCHAR | 40       |                                    | NOT NULL |
| Descripcion      | VARCHAR | 255      |                                    | NOT NULL |
| FechaCreacion    | DATE    |          |                                    | NOT NULL |
| FechaInicio      | DATE    |          |                                    | NOT NULL |
| FechaFin         | DATE    |          |                                    | NOT NULL |
| Creador          | INT     | 11       | FK → usuarios(IdUsuario)           | NOT NULL |
| Subcategoria     | INT     |          | FK → subcategorias(IdSubcategoria) | NOT NULL |
| NumParticipantes | INT     |          |                                    | NOT NULL |
| Direccion        | VARCHAR | 50       |                                    | NOT NULL |
| Localidad        | VARCHAR | 50       |                                    | NOT NULL |
| IdProvincia      | INT     |          | FK → provincias(IdProvincia)       | NOT NULL |
| ModoEvento       | VARCHAR | 11       |                                    | NOT NULL |
| Estado           | VARCHAR | 11       |                                    | NOT NULL |

---

### Provincias 🌍

Esta tabla contiene las provincias disponibles en el sistema.

| Campo       | Tipo    | Longitud | Restricciones      | Null     |
| ----------- | ------- | -------- | ------------------ | -------- |
| IdProvincia | INT     |          | PK AUTOINCREMENTAL | NOT NULL |
| Nombre      | VARCHAR | 50       | UNIQUE             | NOT NULL |

---

### Categorías 🗂️

La tabla de categorías se utiliza para organizar los **eventos** en diferentes categorías, como pueden ser videojuegos, juegos de mesa, deportes, música, etc.

| Campo       | Tipo    | Longitud | Restricciones           | Null     |
| ----------- | ------- | -------- | ----------------------- | -------- |
| IdCategoria | INT     |          | PK AUTOINCREMENTAL      | NOT NULL |
| Nombre      | VARCHAR | 40       | UNIQUE                  | NOT NULL |
| Imagen      | VARCHAR | 40       | DEFAULT 'categoria.svg' | NULL     |

---

### Subcategorías 🗂️

La tabla de subcategorías define los subtipos que pertenecen a una categoría. Por ejemplo, dentro de Videojuegos, puedes tener subcategorías como eSports, Speedrun, Cooperativo, etc.

| Campo          | Tipo    | Longitud | Restricciones                      | Null     |
| -------------- | ------- | -------- | ---------------------------------- | -------- |
| IdSubcategoria | INT     |          | PK AUTOINCREMENTAL                 | NOT NULL |
| IdCategoria    | INT     |          | FK → categorias(IdCategoria)       | NOT NULL |
| Nombre         | VARCHAR | 40       | UNIQUE CON IdCategoria (compuesto) | NOT NULL |

---

### Participantes_Eventos 🔗

Esta tabla intermedia representa la relación **muchos a muchos** entre los usuarios y los eventos a los que se unen.

| Campo     | Tipo | Longitud | Restricciones                | Null     |
| --------- | ---- | -------- | ---------------------------- | -------- |
| IdUsuario | INT  | 11       | PK, FK → usuarios(IdUsuario) | NOT NULL |
| IdEvento  | INT  |          | PK, FK → eventos(IdEvento)   | NOT NULL |

---

## Modificaciones

**Modificaci&oacute;n** - ***(07/04/2025)***
1. Se ha eliminado el campo **Organizador** de la tabla **Usuarios**.
2. Ahora **Organizador** forma parte de `Rol` en la tabla **Usuarios**.
3. El campo **Nombre** de la tabla **Categor&iacute;s** ha pasado a ser `UNIQUE` para evitar creaciones duplicadas.
4. Se ha a&ntilde;adido un estado m&aacute;s al campo `Estado` de la tabla **Eventos** el nuevo estado es `Cancelado`.

---

**Modificaci&oacute;n** - ***(10/04/2025)***
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

---

**Modificaci&oacute;n** - ***(23/04/2025)***
1. **Usuarios:**
   - Se ha eliminado la columna **`puntuacionUser`**.

2. **Eventos:**
   - **Adición de campo `NumParticipantes`**: Se añadió un nuevo campo `NumParticipantes` de tipo `INT`, `NOT NULL`.

---

**Modificaci&oacute;n** - ***(03/05/2025)***
1. **Categorias:**
   - Se ha a&ntilde;adido un nuevo campo `Imagen` para guardar el nombre de la imagen correspondiente. Ej: `deportes.png`
  
2. Se ha creado una nueva tabla `Subcategorias` para mejorar la experiencia de usuario a la hora de crear eventos.

---

**Modificaci&oacute;n** - ***(07/05/2025)***
1. Se ha actualizado los campos de las tablas.

---

**Modificaci&oacute;n** - ***(11/05/2025)***
1. Se ha a&ntilde;adido un nuevo campo en la tabla `Usuarios`.
2. El campo nuevo es `Sexo` y servir&aacute; para controlar la estad&iacute;stica de **Usuarios por Sexo**.

---

**Modificaci&oacute;n** - ***(16/05/2025)***
1. Se ha modificado el nombre de la tabla intermedia `UsuarioEventos` a `Participantes_Eventos` para mejorar la claridad del modelo de datos, reflejando de manera m&aacute;s precisa la relaci&oacute;n entre los usuarios y los eventos en los que participan.

---

**Modificaci&oacute;n** - ***(29/05/2025)***
1. Se ha creado una nueva tabla llamada `Provincias`, que contiene un identificador (`IdProvincia`) y el nombre de la provincia. Esta tabla mejora la integridad referencial y evita la duplicación de nombres de provincias en las tablas relacionadas.

2. En la tabla `Usuarios`, se ha reemplazado el campo `Provincia` por el campo `IdProvincia`, el cual actúa como clave foránea referenciada a `Provincias(IdProvincia)`.

3. En la tabla `Eventos`, también se ha sustituido el campo `Provincia` por `IdProvincia`, estableciendo la relación con la nueva tabla `Provincias` a través de una clave foránea.

---

## ℹ️ Informaci&oacute;n del proyecto:

🧑‍💻**Alumno:** *Alberto Miguel S&aacute;nchez Mac&iacute;as*

🌐**Aplicaci&oacute;n:** *EntreHobbies*

🧑‍🏫**Tutor FCT:** *Francisco Mera Calder&oacute;n*

🏫**Instituto:** *IES Albarregas*

🏫**Clase:** *DAW-2B* 
