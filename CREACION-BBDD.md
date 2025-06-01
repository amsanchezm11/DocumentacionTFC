## Script de Creación de la Base de Datos `entrehobbies`

Este script crea la base de datos `entrehobbies` y las tablas necesarias para gestionar los usuarios, eventos y categorías de la aplicación.
Tambi&eacute;n se han añadido todos los inserts de los datos necesarios para el funcionamiento de la aplicaci&oacute;n.

>[!NOTE]
> - Este documento ha sido creado el d&iacute;a ***10/04/2025*** por ***Alberto Sánchez Macías***.
> - Este documento ha sido actualizado por &uacute;ltima vez el d&iacute;a ***01/06/2025*** por ***Alberto Sánchez Macías***.
## 1. Creación de la Base de Datos

```sql
DROP DATABASE IF EXISTS `entrehobbies`;

CREATE DATABASE /*!32312 IF NOT EXISTS*/ `entrehobbies` /*!40100 DEFAULT CHARACTER SET utf8 COLLATE utf8_spanish_ci */;
```

## 2. Creaci&oacute;n de Usuario y Permisos

### 2.1. Creaci&oacute;n de Usuario Administrador

```sql
DROP USER IF EXISTS 'sanchezadminhobbies'@'localhost';

CREATE USER 'sanchezadminhobbies'@'localhost' IDENTIFIED BY 'AdminHobby*2025+';
```
### 2.2. Asignaci&oacute;n de Permisos al Usuario
```sql
GRANT ALL ON entrehobbies.* TO 'sanchezadminhobbies'@'localhost';
```

## 3. Creaci&oacute;n de las Tablas

### 3.1. Creaci&oacute;n Tabla ***provincias***
```sql
DROP TABLE IF EXISTS `provincias`;

CREATE TABLE `provincias` (
  `IdProvincia` int NOT NULL AUTO_INCREMENT,
  `Nombre` varchar(50) COLLATE utf8_spanish_ci NOT NULL,
  PRIMARY KEY (`IdProvincia`),
  UNIQUE (`Nombre`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_spanish_ci;
```

### 3.2. Creaci&oacute;n Tabla ***categorias***
```sql
DROP TABLE IF EXISTS `categorias`;

CREATE TABLE `categorias` (
  `IdCategoria` INT NOT NULL AUTO_INCREMENT,
  `Nombre` VARCHAR(40) COLLATE utf8_spanish_ci NOT NULL,
  `Imagen` VARCHAR(40) COLLATE utf8_spanish_ci DEFAULT 'categoria.svg',
  PRIMARY KEY (`IdCategoria`),
  UNIQUE (`Nombre`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_spanish_ci;
```

### 3.3. Creaci&oacute;n Tabla ***subcategorias***

```sql
DROP TABLE IF EXISTS `subcategorias`;

CREATE TABLE `subcategorias` (
  `IdSubcategoria` INT NOT NULL AUTO_INCREMENT,
  `IdCategoria` INT NOT NULL,
  `Nombre` VARCHAR(40) COLLATE utf8_spanish_ci NOT NULL,
  PRIMARY KEY (`IdSubcategoria`),
  UNIQUE (`Nombre`, `IdCategoria`),
  CONSTRAINT `fk_subcategoria_categoria`
    FOREIGN KEY (`IdCategoria`) REFERENCES `categorias` (`IdCategoria`)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_spanish_ci;
```

### 3.4. Creaci&oacute;n Tabla ***usuarios***

```sql
DROP TABLE IF EXISTS `usuarios`;

CREATE TABLE `usuarios` (
  `IdUsuario` int(11) NOT NULL AUTO_INCREMENT,
  `Nombre` varchar(30) COLLATE utf8_spanish_ci NOT NULL,
  `Apellidos` varchar(40) COLLATE utf8_spanish_ci NOT NULL,
  `Username` varchar(20) COLLATE utf8_spanish_ci NOT NULL,
  `Email` varchar(60) COLLATE utf8_spanish_ci NOT NULL,
  `Password` varchar(100) COLLATE utf8_spanish_ci NOT NULL,
  `Telefono` varchar(9) COLLATE utf8_spanish_ci NOT NULL,
  `FechaNacimiento` date NOT NULL,
  `Rol` varchar(11) COLLATE utf8_spanish_ci NOT NULL,
  `Sexo` varchar(6) COLLATE utf8_spanish_ci NOT NULL,
  `Localidad` varchar(50) COLLATE utf8_spanish_ci NOT NULL,
  `IdProvincia` int NOT NULL,
  `FechaCreacion` date NOT NULL,
  `Avatar` varchar(30) COLLATE utf8_spanish_ci NOT NULL DEFAULT 'avatar.svg',
  PRIMARY KEY (`IdUsuario`),
  UNIQUE (`Email`),
  UNIQUE (`Username`),
  UNIQUE (`Telefono`),
  CONSTRAINT `fk_usuario_provincia` FOREIGN KEY (`IdProvincia`) REFERENCES `provincias` (`IdProvincia`) ON DELETE RESTRICT ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_spanish_ci;
```

### 3.5. Creaci&oacute;n Tabla ***eventos***

```sql
DROP TABLE IF EXISTS `eventos`;

CREATE TABLE `eventos` (
  `IdEvento` int NOT NULL AUTO_INCREMENT,
  `Titulo` varchar(40) COLLATE utf8_spanish_ci NOT NULL,
  `Descripcion` varchar(255) COLLATE utf8_spanish_ci NOT NULL,
  `FechaCreacion` date NOT NULL,
  `FechaInicio` date NOT NULL,
  `FechaFin` date NOT NULL,
  `Creador` int NOT NULL,
  `Subcategoria` int NOT NULL,
  `NumParticipantes` int NOT NULL,
  `Direccion` varchar(50) COLLATE utf8_spanish_ci NOT NULL,
  `Localidad` varchar(50) COLLATE utf8_spanish_ci NOT NULL,
  `IdProvincia` int NOT NULL,
  `ModoEvento` varchar(11) COLLATE utf8_spanish_ci NOT NULL,
  `Estado` varchar(11) COLLATE utf8_spanish_ci NOT NULL,
  PRIMARY KEY (`IdEvento`),
  FOREIGN KEY (`Creador`) REFERENCES `usuarios` (`IdUsuario`) ON DELETE CASCADE,
  FOREIGN KEY (`Subcategoria`) REFERENCES `subcategorias` (`IdSubcategoria`),
  CONSTRAINT `fk_evento_provincia` FOREIGN KEY (`IdProvincia`) REFERENCES `provincias` (`IdProvincia`) ON DELETE RESTRICT ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_spanish_ci;
```

### 3.6. Creaci&oacute;n Tabla ***participantes_eventos***

```sql
DROP TABLE IF EXISTS `participantes_eventos`;

CREATE TABLE `participantes_eventos` (
  `IdUsuario` INT NOT NULL,
  `IdEvento` INT NOT NULL,
  PRIMARY KEY (`IdUsuario`, `IdEvento`),
  FOREIGN KEY (`IdUsuario`) REFERENCES `usuarios` (`IdUsuario`) ON DELETE CASCADE,
  FOREIGN KEY (`IdEvento`) REFERENCES `eventos` (`IdEvento`) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_spanish_ci;
````

## 4. Creaci&oacute;n de Provincias

### 4.1 INSERT de Provincias

```sql
INSERT INTO `provincias` (`Nombre`) VALUES
('Álava'),
('Albacete'),
('Alicante'),
('Almería'),
('Asturias'),
('Ávila'),
('Badajoz'),
('Barcelona'),
('Burgos'),
('Cáceres'),
('Cádiz'),
('Cantabria'),
('Castellón'),
('Ciudad Real'),
('Córdoba'),
('Cuenca'),
('Gerona'),
('Granada'),
('Guadalajara'),
('Guipúzcoa'),
('Huelva'),
('Huesca'),
('Islas Baleares'),
('Jaén'),
('A Coruña'),
('La Rioja'),
('Las Palmas'),
('León'),
('Lérida'),
('Lugo'),
('Madrid'),
('Málaga'),
('Murcia'),
('Navarra'),
('Orense'),
('Palencia'),
('Pontevedra'),
('Salamanca'),
('Santa Cruz de Tenerife'),
('Segovia'),
('Sevilla'),
('Soria'),
('Tarragona'),
('Teruel'),
('Toledo'),
('Valencia'),
('Valladolid'),
('Vizcaya'),
('Zamora'),
('Zaragoza'),
('Ceuta'),
('Melilla');
```

## 5. Creaci&oacute;n de Usuarios

### 5.1. INSERT de Usuario ***Administrador***

```sql
 INSERT INTO usuarios (
  Nombre, Apellidos, Username, Email, Password, Telefono, FechaNacimiento, Rol, Sexo, Localidad, IdProvincia,FechaCreacion, Avatar
) VALUES (
'Administrador', 'Admin', 'Admin', 'adminhobby@entrehobbies.com', '81dc9bdb52d04dc20036dbd8313ed055',
 '600000000', '1994-03-26', 'Admin', 'Otro', 'Mérida', 7,'2025-01-01', 'admin.svg'
);
```

### 5.2. INSERT de Usuarios ***Colaborador***

```sql
INSERT INTO usuarios (
  Nombre, Apellidos, Username, Email, Password, Telefono,
  FechaNacimiento, Rol, Sexo, Localidad, IdProvincia,FechaCreacion, Avatar
) VALUES
(
  'Laura', 'García Pérez', 'Colaborador1', 'colaborador1@entrehobbies.com', 
  'e10adc3949ba59abbe56e057f20f883e', '600000001', '1995-08-21', 'Colaborador', 'Mujer',
  'Mérida', 7,'2025-01-02', 'avatar.svg'
),
(
  'Carlos', 'Prieto Torres', 'Colaborador2', 'colaborador2@entrehobbies.com',
  'e10adc3949ba59abbe56e057f20f883e', '600000002', '1990-02-10', 'Colaborador', 'Hombre',
  'Mérida', 7,'2025-01-13', 'avatar.svg'
),
(
  'Juan', 'Medina Lopez', 'Colaborador3', 'colaborador3@entrehobbies.com',
  'e10adc3949ba59abbe56e057f20f883e', '600000003', '1992-03-15', 'Colaborador', 'Hombre',
  'Mérida', 7,'2025-04-13', 'avatar.svg'
),
(
  'Ana', 'Ruiz Gómez', 'Colaborador4', 'colaborador4@entrehobbies.com',
  'e10adc3949ba59abbe56e057f20f883e', '600000004', '1994-05-12', 'Colaborador', 'Mujer',
  'Cáceres', 10,'2025-05-10', 'avatar.svg'
),
(
  'Miguel', 'Santos Díaz', 'Colaborador5', 'colaborador5@entrehobbies.com',
  'e10adc3949ba59abbe56e057f20f883e', '600000005', '1988-09-30', 'Colaborador', 'Hombre',
  'Don Benito', 7,'2025-05-01', 'avatar.svg'
),
(
  'Elena', 'Moreno Álvarez', 'Colaborador6', 'colaborador6@entrehobbies.com',
  'e10adc3949ba59abbe56e057f20f883e', '600000006', '1996-11-05', 'Colaborador', 'Mujer',
  'Plasencia', 10,'2025-04-26', 'avatar.svg'
),
(
  'Luis', 'Navarro Pérez', 'Colaborador7', 'colaborador7@entrehobbies.com',
  'e10adc3949ba59abbe56e057f20f883e', '600000007', '1985-06-18', 'Colaborador', 'Hombre',
  'Zafra', 7,'2025-04-20', 'avatar.svg'
),
(
  'Marta', 'López Sánchez', 'Colaborador8', 'colaborador8@entrehobbies.com',
  'e10adc3949ba59abbe56e057f20f883e', '600000008', '1993-04-27', 'Colaborador', 'Mujer',
  'Mérida', 7,'2025-05-15', 'avatar.svg'
),
(
  'Pablo', 'González Ruiz', 'Colaborador9', 'colaborador9@entrehobbies.com',
  'e10adc3949ba59abbe56e057f20f883e', '600000009', '1987-07-14', 'Colaborador', 'Hombre',
  'Coria', 10,'2025-04-06', 'avatar.svg'
),
(
  'Sara', 'Fernández Martín', 'Colaborador10', 'colaborador10@entrehobbies.com',
  'e10adc3949ba59abbe56e057f20f883e', '600000010', '1991-12-01', 'Colaborador', 'Mujer',
  'Almendralejo', 7,'2025-04-10', 'avatar.svg'
);
```

## 6. Creaci&oacute;n de Categor&iacute;as

### 6.1. INSERT de ***Categor&iacute;as***

```sql
INSERT INTO categorias (Nombre, Imagen) VALUES
('Deportes', 'deportes.svg'),
('Juegos de mesa', 'juegosdemesa.svg'),
('Videojuegos', 'videojuegos.svg'),
('Lectura y literatura', 'lecturayliteratura.svg'),
('Teatro y Cine', 'teatroycine.svg'),
('Música y Danza', 'musicaydanza.svg'),
('Eventos y Ferias', 'eventosyferias.svg'),
('Creatividad y Manualidades', 'creatividadymanualidades.svg'),
('Naturaleza y Bienestar', 'naturalezaybienestar.svg'),
('Conocimiento y Desarrollo Personal', 'conocimientoydesarrollopersonal.svg'),
('Moda y Estilo', 'modayestilo.svg'),
('Coleccionismo', 'coleccionismo.svg'),
('Tecnología', 'tecnologia.svg'),
('Turismo', 'turismo.svg'),
('Cocina y Gastronomía', 'cocinaygastronomia.svg');
```

## 7. Creaci&oacute;n de Subcategor&iacute;as

### 7.1. Insert de ***Subcategor&iacute;as***

```sql
INSERT INTO subcategorias (IdCategoria, Nombre) VALUES
-- Deportes (1)
(1, 'Otro - Deportes'),
(1, 'Fútbol'),
(1, 'Tenis'),
(1, 'Pádel'),
(1, 'Baloncesto'),
(1, 'Ciclismo'),
(1, 'Running'),
(1, 'Senderismo'),
(1, 'Gimnasio'),
(1, 'Crossfit'),
(1, 'Skateboarding'),
(1, 'Artes marciales'),
(1, 'Boxeo'),
(1, 'Natación'),
-- Juegos de mesa (2)
(2, 'Otro - Juegos de mesa'),
(2, 'Ajedrez'),
(2, 'Magic: The Gathering'),
(2, 'Pokémon TCG'),
(2, 'Yu-Gi-Oh! TCG'),
(2, 'Warhammer 40K'),
(2, 'Juegos de rol'),
(2, 'Catan'),
(2, 'Dixit'),
(2, 'Intercambio de cartas'),
-- Videojuegos (3)
(3, 'Otro - Videojuegos'),
(3, 'Torneos presenciales'),
(3, 'Cooperativo'),
(3, 'Casual'),
(3, 'Competitivo'),
(3, 'Streaming'),
(3, 'Retro gaming'),
(3, 'Pokémon GO'),
-- Lectura y literatura (4)
(4, 'Otro - Lectura y literatura'),
(4, 'Club de lectura'),
(4, 'Lectura conjunta'),
(4, 'Firmas de libros'),
(4, 'Talleres de escritura'),
(4, 'Encuentros con autores'),
(4, 'Literatura'),
-- Teatro y Cine (5)
(5, 'Otro - Teatro y Cine'),
(5, 'Cine'),
(5, 'Maratón de películas'),
(5, 'Cine Documental y Debates'),
(5, 'Teatro'),
(5, 'Musicales'),
(5, 'Cine al aire libre'),
(5, 'Talleres de actuación'),
-- Música y Danza (6)
(6, 'Otro - Música y Danza'),
(6, 'Conciertos'),
(6, 'Clases de baile'),
(6, 'Micro abierto'),
(6, 'Música en vivo'),
(6, 'Ópera'),
(6, 'Ballet'),
(6, 'Música folclórica'),
(6, 'Danza'),
-- Eventos y Ferias (7)
(7, 'Otro - Eventos y Ferias'),
(7, 'Ferias del libro'),
(7, 'Festivales frikis y gaming'),
(7, 'Ferias del vinilo'),
(7, 'Ferias tecnológicas'),
(7, 'Mercadillo'),
(7, 'Festivales de arte'),
(7, 'Mercados medievales'),
(7, 'Cosplay'),
(7, 'Eventos culturales'),
-- Creatividad y Manualidades (8)
(8, 'Otro - Creatividad y Manualidades'),
(8, 'Manualidades'),
(8, 'Pintura'),
(8, 'Dibujo'),
(8, 'Fotografía'),
(8, 'Modelismo'),
(8, 'Cerámica'),
(8, 'Lettering'),
(8, 'Scrapbooking'),
-- Naturaleza y Bienestar (9)
(9, 'Otro - Naturaleza y Bienestar'),
(9, 'Jardinería'),
(9, 'Senderismo'),
(9, 'Meditación'),
(9, 'Yoga'),
(9, 'Observación de aves'),
(9, 'Acampada'),
(9, 'Paseo'),
-- Conocimiento y Desarrollo Personal (10)
(10, 'Otro - Conocimiento y DP'),
(10, 'Aprender idiomas'),
(10, 'Desarollo Personal'),
(10, 'Club de debate'),
(10, 'Ciencia y tecnología'),
(10, 'Historia'),
(10, 'Escritura creativa'),
-- Moda y Estilo (11)
(11, 'Otro - Moda y Estilo'),
(11, 'Moda sostenible'),
(11, 'Tejido y ganchillo'),
(11, 'Costura creativa'),
(11, 'Costura'),
(11, 'Estilísmo'),
(11, 'Maquillaje'),
(11, 'Customización de ropa'),
-- Coleccionismo (12)
(12, 'Otro - Coleccionismo'),
(12, 'Figuras'),
(12, 'Sellos'),
(12, 'Monedas'),
(12, 'Consolas retro'),
(12, 'Cartas coleccionables'),
(12, 'Vinilos'),
(12, 'Cómics y mangas'),
(12, 'Colecciones temáticas'),
-- Tecnología (13)
(13, 'Otro - Tecnología'),
(13, 'Programación y desarrollo'),
(13, 'Tecnología'),
(13, 'Taller de Robótica'),
(13, 'Taller de Impresión 3D'),
(13, 'Drones'),
(13, 'Domótica y hogar inteligente'),
(13, 'Inteligencia Artificial'),
(13, 'Café tecnológico (debates y novedades)'),
-- Turismo (14)
(14, 'Otro - Turismo'),
(14, 'Visitas Guiadas'),
(14, 'Freetour Cultural'),
(14, 'Excursiones'),
(14, 'Turismo Rural'),
(14, 'Visitas a Museos'),
-- Cocina y gastronomía (15)
(15, 'Otro - Cocina y gastronomía'),
(15, 'Cocina'),
(15, 'Gastronomía'),
(15, 'Pastelería y Repostería'),
(15, 'Taller de Cocina'),
(15, 'Cata Gourmet'),
(15, 'Barbacoa');
```

## 8. Creaci&oacute;n de eventos

### 8.1. Insert de ***Eventos***

```sql
INSERT INTO eventos (Titulo, Descripcion, FechaCreacion, FechaInicio, FechaFin, Creador, Subcategoria, NumParticipantes, Direccion, Localidad, IdProvincia, ModoEvento, Estado) VALUES
-- Deportes (1)
('Quedada de senderismo', 'Plan sin presiones para disfrutar juntos de senderismo. ¡Te esperamos!', '2025-05-13', '2025-05-13', '2025-05-14', 2, 8, 6, 'Calle Mayor, 19', 'Torrent', 46, 'Comunitario', 'Finalizado'),
('Descubre senderismo', 'Plan sin presiones para disfrutar juntos de senderismo. ¡Te esperamos!', '2025-05-12', '2025-06-13', '2025-06-14', 2, 8, 11, 'Plaza de España, 21', 'Torrent', 46, 'Comunitario', 'Por_Empezar'),
('Torneo de Pádel Primavera', 'Competencia amistosa de pádel por parejas para fomentar el deporte y el compañerismo.', '2025-05-01', '2025-05-03', '2025-05-03', 3, 4, 16, 'Club Deportivo La Raqueta, Ctra. Sevilla s/n', 'Sevilla', 41, 'Comunitario', 'Finalizado'),
('Fútbol Sala entre Amigos', 'Partido de fútbol sala entre vecinos y aficionados. Se formarán equipos al llegar.', '2025-05-05', '2025-05-10', '2025-05-10', 14, 2, 14, 'Polideportivo Municipal San Juan', 'Granada', 18, 'Comunitario', 'Finalizado'),
('Tarde de Baloncesto en el Barrio', 'Jornada deportiva de baloncesto en equipo. Ideal para jóvenes y adultos que quieran pasar un buen rato jugando.', '2025-05-07', '2025-05-12', '2025-05-12', 3, 5, 10, 'Pista Deportiva Parque Norte', 'Málaga', 32, 'Comunitario', 'Finalizado'),
-- Juegos de mesa (2)
('Taller de ajedrez', 'Un encuentro relajado para hablar y explorar ajedrez. ¡Te esperamos!', '2025-04-28', '2025-04-28', '2025-04-29', 2, 16, 7, 'Calle Nueva, 109', 'Zaragoza', 50, 'Comunitario', 'Finalizado'),
('Actividad sobre ajedrez', 'Acércate y disfruta de una experiencia sobre ajedrez. ¡Te esperamos!', '2025-04-07', '2025-04-07', '2025-04-08', 2, 16, 6, 'Plaza de España, 85', 'Plasencia', 10, 'Comunitario', 'Finalizado'),
-- Videojuegos (3)
('Torneo Smash Bros Ultimate', 'Compite en nuestro torneo presencial de Super Smash Bros Ultimate. Premios para los primeros puestos.', '2025-01-05', '2025-01-20', '2025-01-20', 3, 29, 16, 'Calle Gamer 12', 'Sevilla', 41, 'Comunitario', 'Finalizado'),
('Quedada Overwatch 2 - Modo Arcade', 'Evento online para disfrutar de partidas arcade y cooperativas en Overwatch 2. Únete desde casa.', '2025-01-10', '2025-01-22', '2025-01-22', 3, 27, 10, 'Online', 'Madrid', 31, 'Comunitario', 'Finalizado'),
('Speedrun de Zelda: Breath of the Wild', 'Stream especial de speedrunning donde varios jugadores competirán por el mejor tiempo.', '2025-01-15', '2025-01-25', '2025-01-25', 3, 30, 8, 'Twitch.tv/zeldaevent', 'Valencia', 46, 'Comunitario', 'Finalizado'),
('Conoce más de videojuegos', 'Sesión participativa donde profundizaremos en videojuegos. ¡Te esperamos!', '2025-05-23', '2025-06-23', '2025-06-24', 3, 25, 8, 'Plaza de España, 16', 'Motril', 18, 'Comunitario', 'Por_Empezar'),
-- Lectura y literatura (4)
('Club de lectura mensual', 'Lectura compartida de una novela clásica cada mes.', '2025-05-07', '2025-06-01', '2025-08-01', 3, 34, 12, 'Biblioteca Central, Sala 3', 'Cáceres', 10, 'Comunitario', 'Por_Empezar'),
('Taller de escritura creativa', 'Explora técnicas narrativas y crea tus propios relatos.', '2025-05-28', '2025-05-29', '2025-06-15', 2, 37, 15, 'Casa de Cultura, Aula 2', 'Plasencia', 10, 'Comunitario', 'En_Curso'),
('Club de lectura mensual', 'Lectura compartida de una novela negra cada mes.', '2025-05-07', '2025-06-01', '2025-08-01', 3, 34, 12, 'Biblioteca Central, Sala 3', 'Cáceres', 10, 'Comunitario', 'Por_Empezar'),
('Taller de escritura creativa avanzada', 'Explora técnicas narrativas más avanzadas y crea tus propios relatos.', '2025-05-07', '2025-06-05', '2025-07-10', 2, 37, 15, 'Casa de Cultura, Aula 2', 'Plasencia', 10, 'Comunitario', 'Por_Empezar'),
('Lectura conjunta de novela negra', 'Lectura y análisis grupal de una novela policiaca.', '2025-05-10', '2025-06-20', '2025-07-20', 3, 35, 10, 'Centro de Ocio Joven', 'Coria', 10, 'Comunitario', 'Por_Empezar'),
('Tarde de poesía en voz alta', 'Lectura y recitación de poesía contemporánea.', '2025-05-10', '2025-06-22', '2025-06-22', 3, 33, 25, 'Ateneo Cultural', 'Miajadas', 10, 'Comunitario', 'Por_Empezar'),
('Encuentro con autor extremeño', 'Presentación de obra y firma de libros.', '2025-05-10', '2025-06-25', '2025-06-25', 3, 38, 40, 'Librería Nueva', 'Navalmoral de la Mata', 10, 'Comunitario', 'Por_Empezar'),
('Taller de microrrelatos', 'Escribe historias impactantes en menos de 200 palabras.', '2025-05-10', '2025-07-01', '2025-07-15', 2, 33, 18, 'Centro Cultural La Nave', 'Cáceres', 10, 'Comunitario', 'Por_Empezar'),
('Club de lectura juvenil', 'Sesiones quincenales para jóvenes lectores.', '2025-05-10', '2025-06-10', '2025-09-01', 3, 34, 16, 'Biblioteca Municipal', 'Trujillo', 10, 'Comunitario', 'Por_Empezar'),
('Taller de lectura', 'Acércate y disfruta de una experiencia sobre lectura. ¡Te esperamos!', '2025-05-18', '2025-05-18', '2025-05-19', 3, 35, 1, 'Calle Mayor, 55', 'Mataró', 8, 'Comunitario', 'Por_Empezar'),
('Conoce más de escritura', 'Un encuentro relajado para hablar y explorar escritura. ¡Te esperamos!', '2025-05-23', '2025-05-25', '2025-05-26', 2, 37, 6, 'Plaza de España, 30', 'Mataró', 8, 'Comunitario', 'Por_Empezar'),
('Explorando cómics', 'Plan sin presiones para disfrutar juntos de cómics. ¡Te esperamos!', '2025-05-21', '2025-05-27', '2025-05-28', 3, 35, 11, 'Avenida del Sol, 31', 'Dos Hermanas', 41, 'Comunitario', 'Por_Empezar'),
('Charla de cómics', 'Plan sin presiones para disfrutar juntos de cómics. ¡Te esperamos!', '2025-04-29', '2025-04-29', '2025-04-30', 3, 39, 9, 'Avenida del Sol, 88', 'Mérida', 7, 'Comunitario', 'Por_Empezar'),
('Evento especial:  escritura', 'Sesión participativa donde profundizaremos en escritura. ¡Te esperamos!', '2025-04-30', '2025-04-30', '2025-05-01', 3, 37, 9, 'Calle Jardín, 58', 'Ferrol', 25, 'Comunitario', 'Por_Empezar'),
-- Teatro y Cine (5)
('Descubre cine', 'Actividad ideal para quienes se interesan por cine. ¡Te esperamos!', '2025-05-19', '2025-05-19', '2025-05-20', 2, 42, 8, 'Avenida del Sol, 5', 'Barcelona', 8, 'Comunitario', 'Finalizado'),
('Actividad sobre cine', 'Una oportunidad perfecta para compartir nuestra pasión por cine. ¡Te esperamos!', '2025-04-25', '2025-04-25', '2025-04-26', 2, 41, 5, 'Plaza de España, 51', 'Getafe', 31, 'Comunitario', 'Finalizado'),
('Iniciación a cine', 'Si te llama la atención el mundo de cine. ¡Te esperamos!', '2025-05-23', '2025-06-23', '2025-06-24', 2, 41, 9, 'Calle Jardín, 26', 'Zaragoza', 50, 'Comunitario', 'Por_Empezar'),
('Noche de cortometrajes', 'Proyección y debate de cortos independientes.', '2025-05-07', '2025-05-10', '2025-05-20', 3, 43, 30, 'Centro Cultural El Brocense', 'Cáceres', 10, 'Comunitario', 'En_Curso'),
('Taller de iniciación al teatro', 'Dinámicas para perder el miedo escénico y desarrollar habilidades actorales.', '2025-05-07', '2025-06-15', '2025-07-20', 2, 44, 20, 'Espacio para la Creación Joven', 'Navalmoral de la Mata', 10, 'Comunitario', 'Por_Empezar'),
('Noche de cortometrajes', 'Proyección y debate de cortos independientes.', '2025-05-07', '2025-06-10', '2025-06-10', 3, 42, 30, 'Centro Cultural El Brocense', 'Cáceres', 10, 'Comunitario', 'Por_Empezar'),
('Taller de iniciación al teatro', 'Dinámicas para perder el miedo escénico y desarrollar habilidades actorales.', '2025-05-25', '2025-05-25', '2025-07-30', 2, 44, 20, 'Espacio para la Creación Joven', 'Navalmoral de la Mata', 10, 'Comunitario', 'En_Curso'),
('Visionado comentado de clásicos', 'Proyección de películas clásicas con análisis posterior.', '2025-05-10', '2025-06-12', '2025-06-12', 3, 43, 35, 'Filmoteca de Extremadura', 'Plasencia', 10, 'Comunitario', 'Por_Empezar'),
('Taller de monólogos teatrales', 'Aprende a escribir y representar tu propio monólogo.', '2025-05-10', '2025-06-20', '2025-07-25', 3, 44, 15, 'Casa de Cultura', 'Moraleja', 10, 'Comunitario', 'Por_Empezar'),
('Festival de teatro aficionado', 'Muestra de obras teatrales de grupos locales.', '2025-05-10', '2025-07-10', '2025-07-12', 3, 44, 50, 'Teatro Alkázar', 'Plasencia', 10, 'Comunitario', 'Por_Empezar'),
('Cine al aire libre', 'Proyección nocturna de películas para todos los públicos.', '2025-05-10', '2025-07-01', '2025-07-01', 2, 46, 100, 'Parque del Príncipe', 'Cáceres', 10, 'Comunitario', 'Por_Empezar'),
('Taller de dirección escénica', 'Conceptos básicos de puesta en escena y dirección.', '2025-05-10', '2025-07-15', '2025-08-15', 3, 41, 12, 'Espacio Creativo', 'Coria', 10, 'Comunitario', 'Por_Empezar'),
('Charla de teatro', 'Plan sin presiones para disfrutar juntos de teatro. ¡Te esperamos!', '2025-05-04', '2025-05-04', '2025-05-05', 3, 44, 12, 'Calle Jardín, 32', 'Leganés', 31, 'Comunitario', 'Finalizado'),
-- Música y Danza (6)
('Jam session abierta', 'Ven con tu instrumento o voz a improvisar con otros músicos.', '2025-05-07', '2025-06-20', '2025-06-20', 3, 52, 30, 'Sala Boogaloo', 'Cáceres', 10, 'Comunitario', 'Por_Empezar'),
('Taller de bailes latinos', 'Aprende los pasos básicos de salsa, bachata y merengue.', '2025-05-07', '2025-06-18', '2025-07-30', 2, 56, 20, 'Academia Ritmo Tropical', 'Plasencia', 10, 'Comunitario', 'Por_Empezar'),
('Iniciación a música en vivo', 'Si te llama la atención el mundo de música en vivo. ¡Te esperamos!', '2025-04-27', '2025-04-27', '2025-04-28', 3, 52, 2, 'Calle Nueva, 24', 'A Coruña', 25, 'Comunitario', 'Finalizado'),
('Iniciación a música en vivo', 'Actividad ideal para quienes se interesan por música en vivo. ¡Te esperamos!', '2025-05-08', '2025-06-18', '2025-06-19', 2, 52, 12, 'Avenida del Sol, 113', 'Utebo', 50, 'Comunitario', 'Por_Empezar'),
('Iniciación a baile', 'Si te llama la atención el mundo de baile. ¡Te esperamos!', '2025-05-17', '2025-06-17', '2025-06-18', 2, 50, 5, 'Calle Mayor, 101', 'A Coruña', 25, 'Comunitario', 'Por_Empezar'),
('Clases de baile', 'Nos reuniremos para aprender y disfrutar sobre baile. ¡Te esperamos!', '2025-04-06', '2025-04-06', '2025-04-07', 2, 50, 3, 'Avenida del Sol, 101', 'Torrent', 46, 'Comunitario', 'Finalizado'),
('Sesión abierta de música en vivo', 'Plan sin presiones para disfrutar juntos de música en vivo. ¡Te esperamos!', '2025-04-30', '2025-04-30', '2025-05-01', 3, 52, 6, 'Avenida del Sol, 100', 'Getafe', 31, 'Comunitario', 'Finalizado'),
('Iniciación a baile', 'Una oportunidad perfecta para compartir nuestra pasión por baile. ¡Te esperamos!', '2025-04-04', '2025-04-04', '2025-04-05', 3, 50, 11, 'Calle Nueva, 36', 'Badajoz', 7, 'Comunitario', 'Finalizado'),
-- Eventos y Ferias (7)
('Feria medieval local', 'Puestos, representaciones y música ambientada en la Edad Media.', '2025-05-07', '2025-08-01', '2025-08-03', 2, 64, 100, 'Casco Antiguo', 'Cáceres', 10, 'Comunitario', 'Por_Empezar'),
('Encuentro cosplay y cultura friki', 'Ven disfrazado de tu personaje favorito y participa en concursos.', '2025-05-07', '2025-07-15', '2025-07-15', 2, 59, 50, 'Palacio de Congresos', 'Cáceres', 10, 'Comunitario', 'Por_Empezar'),
-- Creatividad y Manualidades (8)
('Conoce más de artesanía', 'Actividad ideal para quienes se interesan por artesanía. ¡Te esperamos!', '2025-05-14', '2025-05-14', '2025-05-15', 2, 68, 5, 'Avenida del Sol, 104', 'Utebo', 50, 'Comunitario', 'Finalizado'),
('Evento especial:  manualidades', 'Si te llama la atención el mundo de manualidades. ¡Te esperamos!', '2025-04-03', '2025-04-03', '2025-04-04', 3, 68, 9, 'Plaza de España, 49', 'Mataró', 8, 'Comunitario', 'Finalizado'),
('Actividad sobre artesanía', 'Plan sin presiones para disfrutar juntos de artesanía. ¡Te esperamos!', '2025-05-06', '2025-05-06', '2025-05-07', 3, 68, 2, 'Plaza de España, 111', 'Valencia', 46, 'Comunitario', 'Finalizado'),
('Quedada de manualidades', 'Actividad ideal para quienes se interesan por manualidades. ¡Te esperamos!', '2025-05-12', '2025-05-12', '2025-05-13', 3, 68, 4, 'Calle Jardín, 46', 'A Coruña', 25, 'Comunitario', 'Finalizado'),
('Explorando fotografía', 'Plan sin presiones para disfrutar juntos de fotografía. ¡Te esperamos!', '2025-05-23', '2025-05-23', '2025-05-24', 3, 71, 1, 'Calle Jardín, 102', 'Mérida', 7, 'Comunitario', 'Finalizado'),
('Descubre manualidades', 'Nos reuniremos para aprender y disfrutar sobre manualidades. ¡Te esperamos!', '2025-05-23', '2025-05-29', '2025-06-15', 3, 68, 7, 'Avenida del Sol, 53', 'Utebo', 50, 'Comunitario', 'En_Curso'),
('Charla de manualidades', 'Plan sin presiones para disfrutar juntos de manualidades. ¡Te esperamos!', '2025-05-20', '2025-05-29', '2025-06-20', 2, 68, 6, 'Plaza de España, 3', 'Barcelona', 8, 'Comunitario', 'En_Curso'),
('Taller de manualidades', 'Plan sin presiones para disfrutar juntos de manualidades. ¡Te esperamos!', '2025-04-24', '2025-04-24', '2025-04-25', 2, 68, 4, 'Avenida del Sol, 94', 'Leganés', 31, 'Comunitario', 'Finalizado'),
-- Naturaleza y Bienestar (9)
('Ruta Verde por Sierra Morena', 'Jornada de ovservación de aves para explorar rutas naturales y fomentar la vida activa en grupo.', '2025-04-01', '2025-04-06', '2025-04-06', 2, 81, 25, 'Área Recreativa El Mirador, Km 12', 'Córdoba', 15, 'Comunitario', 'Finalizado'),
('Yoga en el Parque del Retiro', 'Sesión grupal de yoga para mejorar el bienestar físico y mental. Abierto a todos los niveles.', '2025-04-04', '2025-04-10', '2025-04-10', 2, 80, 30, 'Parque del Retiro, Entrada Puerta de Alcalá', 'Madrid', 31, 'Comunitario', 'Finalizado'),
('Encuentro de Meditación y Mindfulness', 'Sesión de meditación guiada al aire libre para fomentar la paz interior y la conexión grupal.', '2025-04-08', '2025-04-14', '2025-04-14', 3, 79, 20, 'Jardín Botánico, Paseo del Prado 2', 'Madrid', 31, 'Comunitario', 'Finalizado'),
-- Conocimiento y Desarrollo Personal (10)
('Iniciación a historia', 'Plan sin presiones para disfrutar juntos de historia. ¡Te esperamos!', '2025-05-28', '2025-05-28', '2025-05-29', 3, 89, 9, 'Calle Nueva, 56', 'Getafe', 31, 'Comunitario', 'Finalizado'),
('Charla de ciencia', 'Si te llama la atención el mundo de ciencia. ¡Te esperamos!', '2025-05-02', '2025-05-02', '2025-05-03', 3, 88, 9, 'Calle Nueva, 64', 'Cáceres', 10, 'Comunitario', 'Finalizado'),
('Charla de ciencia', 'Plan sin presiones para disfrutar juntos de ciencia. ¡Te esperamos!', '2025-04-08', '2025-04-08', '2025-04-09', 3, 88, 12, 'Plaza de España, 39', 'Badajoz', 7, 'Comunitario', 'Finalizado'),
('Iniciación a conversación', 'Sesión participativa donde profundizaremos en conversación. ¡Te esperamos!', '2025-04-12', '2025-04-12', '2025-04-13', 2, 86, 10, 'Calle Mayor, 2', 'Ferrol', 25, 'Comunitario', 'Finalizado'),
('Sesión abierta de ciencia', 'Plan sin presiones para disfrutar juntos de ciencia. ¡Te esperamos!', '2025-04-21', '2025-04-21', '2025-04-22', 2, 88, 11, 'Avenida del Sol, 85', 'Valencia', 46, 'Comunitario', 'Finalizado'),
('Actividad sobre debate', 'Un encuentro relajado para hablar y explorar debate. ¡Te esperamos!', '2025-05-24', '2025-06-19', '2025-06-20', 2, 87, 9, 'Avenida del Sol, 101', 'Ferrol', 25, 'Comunitario', 'Por_Empezar'),
('Charla de ciencia', 'Plan sin presiones para disfrutar juntos de ciencia. ¡Te esperamos!', '2025-05-06', '2025-05-06', '2025-05-07', 2, 88, 10, 'Calle Jardín, 84', 'Mataró', 8, 'Comunitario', 'Finalizado'),
('Evento especial:  historia', 'Un encuentro relajado para hablar y explorar historia. ¡Te esperamos!', '2025-05-09', '2025-05-09', '2025-05-10', 2, 89, 9, 'Calle Nueva, 23', 'Mérida', 7, 'Comunitario', 'Finalizado'),
('Charla de ciencia', 'Una oportunidad perfecta para compartir nuestra pasión por ciencia. ¡Te esperamos!', '2025-04-26', '2025-04-26', '2025-04-27', 3, 88, 3, 'Avenida del Sol, 50', 'Zaragoza', 50, 'Comunitario', 'Finalizado'),
-- Moda y Estilo (11)
('Desfile de Moda Urbana', 'Evento exclusivo con diseñadores emergentes de moda urbana. Pasarela y networking.', '2025-02-08', '2025-02-18', '2025-02-18', 3, 92, 50, 'Paseo de la Moda 45', 'Barcelona', 8, 'Comunitario', 'Finalizado'),
('Taller de Maquillaje Natural', 'Aprende técnicas básicas y avanzadas para un maquillaje de día fresco y profesional.', '2025-02-12', '2025-02-20', '2025-02-20', 3, 97, 15, 'Av. Belleza 22', 'Granada', 18, 'Comunitario', 'Finalizado'),
('Asesoría de Imagen Express', 'Sesiones individuales para mejorar tu estilo personal con asesoras expertas.', '2025-02-03', '2025-02-10', '2025-02-10', 2, 96, 8, 'Calle Estilo 5', 'Valencia', 46, 'Comunitario', 'Finalizado'),
-- Coleccionismo (12)
('Encuentro Numismático 2025', 'Reunión comunitaria para mostrar, intercambiar y aprender sobre monedas históricas.', '2025-03-01', '2025-03-08', '2025-03-08', 3, 102, 20, 'Centro Cultural Antigüedades, Calle Real 10', 'Madrid', 31, 'Comunitario', 'Finalizado'),
('Expo Juguetes Retro', 'Muestra de juguetes vintage de los años 60 a 90. Actividades para todas las edades.', '2025-03-05', '2025-03-15', '2025-03-15', 3, 100, 35, 'Pabellón Nostalgia, Av. de la Infancia 22', 'Zaragoza', 50, 'Comunitario', 'Finalizado'),
('Tarde Filatélica', 'Evento para aficionados a la filatelia. Intercambios, charlas y exposiciones de sellos raros.', '2025-03-10', '2025-03-20', '2025-03-20', 3, 101, 18, 'Sala de Aficiones, Plaza Mayor 3', 'Sevilla', 41, 'Comunitario', 'Finalizado'),
-- Tecnología (13)
('Sesión abierta de tecnología', 'Nos reuniremos para aprender y disfrutar sobre tecnología. ¡Te esperamos!', '2025-04-01', '2025-04-01', '2025-04-02', 2, 110, 4, 'Avenida del Sol, 72', 'Leganés', 31, 'Comunitario', 'Finalizado'),
('Descubre tecnología', 'Una oportunidad perfecta para compartir nuestra pasión por tecnología. ¡Te esperamos!', '2025-05-14', '2025-05-14', '2025-05-15', 3, 110, 5, 'Calle Nueva, 16', 'Getafe', 31, 'Comunitario', 'Finalizado'),
('Evento especial:  tecnología', 'Un encuentro relajado para hablar y explorar tecnología. ¡Te esperamos!', '2025-04-24', '2025-04-24', '2025-04-25', 3, 110, 5, 'Calle Jardín, 74', 'A Coruña', 25, 'Comunitario', 'Finalizado'),
-- Turismo (14)
('Charla de viajes', 'Actividad ideal para quienes se interesan por viajes. ¡Te esperamos!', '2025-05-06', '2025-05-30', '2025-05-31', 3, 117, 2, 'Plaza de España, 90', 'Badajoz', 7, 'Comunitario', 'Por_Empezar'),
('Ruta por el casco histórico', 'Recorrido guiado por los puntos clave del patrimonio de la ciudad.', '2025-06-07', '2025-06-17', '2025-06-18', 3, 120, 25, 'Plaza Mayor', 'Trujillo', 10, 'Comunitario', 'Por_Empezar'),
('Visita a exposición contemporánea', 'Análisis colectivo de obras de arte moderno en galería local.', '2025-05-07', '2025-06-12', '2025-06-12', 2, 118, 20, 'Galería Arte XXI', 'Cáceres', 10, 'Comunitario', 'Por_Empezar'),
-- Cocina y gastronomía (15)
('Explorando gastronomía', 'Plan sin presiones para disfrutar juntos de gastronomía. ¡Te esperamos!', '2025-04-26', '2025-04-26', '2025-04-27', 2, 125, 7, 'Plaza de España, 76', 'Sevilla', 41, 'Comunitario', 'Finalizado'),
('Conoce más de gastronomía', 'Una oportunidad perfecta para compartir nuestra pasión por gastronomía. ¡Te esperamos!', '2025-04-09', '2025-04-09', '2025-04-10', 2, 125, 11, 'Calle Mayor, 93', 'Mérida', 7, 'Comunitario', 'Finalizado'),
('Conoce más de gastronomía', 'Un encuentro relajado para hablar y explorar gastronomía. ¡Te esperamos!', '2025-05-03', '2025-05-24', '2025-05-26', 2, 125, 4, 'Calle Nueva, 97', 'Plasencia', 10, 'Comunitario', 'Finalizado');
```

## 9. Creaci&oacute;n de participantes
### 9.1 INSERT de participantes
```sql
INSERT INTO participantes_eventos (IdUsuario, IdEvento) VALUES
(10, 32),
(5, 32),
(6, 29),
(11, 29),
(7, 29),
(3, 13),
(4, 13),
(5, 13),
(4, 54),
(10, 54),
(9, 55),
(6, 55);
```
