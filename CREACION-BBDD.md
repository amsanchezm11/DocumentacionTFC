## Script de Creación de la Base de Datos `entrehobbies`

Este script crea la base de datos `entrehobbies` y las tablas necesarias para gestionar los usuarios, eventos y categorías de la aplicación.

Este documento ha sido creado el día ***10/04/2025*** por ***Alberto Sánchez Macías***.

## 1. Creación de la Base de Datos

```sql
DROP DATABASE IF EXISTS `entrehobbies`;

CREATE DATABASE /*!32312 IF NOT EXISTS*/ `entrehobbies` /*!40100 DEFAULT CHARACTER SET utf8 COLLATE utf8_spanish_ci */;
```

## 2. Creación de Usuario y Permisos

### 2.1. Creación de Usuario Administrador

```sql
DROP USER IF EXISTS 'sanchezadminhobbies'@'localhost';

CREATE USER 'sanchezadminhobbies'@'localhost' IDENTIFIED BY 'AdminHobby*2025+';
```
### 2.2. Asignación de Permisos al Usuario
```sql
GRANT ALL ON entrehobbies.* TO 'sanchezadminhobbies'@'localhost';
```

## 3. Creación de las Tablas

### 3.1. Creación Tabla ***categorias***
```sql
DROP TABLE IF EXISTS `categorias`;

CREATE TABLE `categorias` (
  `IdCategoria` int NOT NULL AUTO_INCREMENT,
  `Nombre` varchar(40) COLLATE utf8_spanish_ci NOT NULL,
  `Imagen` varchar(40) COLLATE utf8_spanish_ci DEFAULT 'categoria.svg',
  PRIMARY KEY (`IdCategoria`),
  UNIQUE (`Nombre`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_spanish_ci;
```

### 3.2. Creación Tabla ***subcategorias***

```sql
DROP TABLE IF EXISTS `subcategorias`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `subcategorias` (
  `IdSubcategoria` int NOT NULL AUTO_INCREMENT,
  `IdCategoria` int NOT NULL,
  `Nombre` varchar(40) COLLATE utf8_spanish_ci NOT NULL,
  PRIMARY KEY (`IdSubcategoria`),
  UNIQUE (`Nombre`, `IdCategoria`),
  CONSTRAINT `fk_subcategoria_categoria` FOREIGN KEY (`IdCategoria`) REFERENCES `categorias` (`IdCategoria`)
    ON DELETE CASCADE
    ON UPDATE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_spanish_ci;
/*!40101 SET character_set_client = @saved_cs_client */;
```

### 3.3. Creación Tabla ***usuarios***

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
  `Provincia` varchar(50) COLLATE utf8_spanish_ci NOT NULL,
  `Avatar` varchar(30) COLLATE utf8_spanish_ci NOT NULL DEFAULT 'avatar.svg',
  PRIMARY KEY (`IdUsuario`),
  UNIQUE (`Email`),
  UNIQUE (`Username`),
  UNIQUE (`Telefono`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_spanish_ci;
```

### 3.4. Creación Tabla ***eventos***

```sql
DROP TABLE IF EXISTS `eventos`;

CREATE TABLE `eventos` (
  `IdEvento` int NOT NULL AUTO_INCREMENT,
  `Titulo` varchar(40) COLLATE utf8_spanish_ci NOT NULL,
  `Descripcion` varchar(100) COLLATE utf8_spanish_ci NOT NULL,
  `FechaCreacion` date NOT NULL,
  `FechaInicio` date NOT NULL,
  `FechaFin` date NOT NULL,
  `Creador` int NOT NULL,
  `Categoria` int NOT NULL,
  `NumParticipantes` int NOT NULL,
  `Direccion` varchar(50) COLLATE utf8_spanish_ci NOT NULL,
  `Localidad` varchar(50) COLLATE utf8_spanish_ci NOT NULL,
  `Provincia` varchar(50) COLLATE utf8_spanish_ci NOT NULL,
  `ModoEvento` varchar(11) COLLATE utf8_spanish_ci NOT NULL,
  `Estado` varchar(11) COLLATE utf8_spanish_ci NOT NULL,
  PRIMARY KEY (`IdEvento`),
  FOREIGN KEY (`Creador`) REFERENCES `usuarios` (`IdUsuario`) ON DELETE CASCADE,
  FOREIGN KEY (`Categoria`) REFERENCES `categorias` (`IdCategoria`) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_spanish_ci;
```

### 3.5. Creación Tabla ***usuarioeventos***

```sql
DROP TABLE IF EXISTS `usuarioeventos`;

CREATE TABLE `usuarioeventos` (
  `IdUsuario` int NOT NULL,
  `IdEvento` int NOT NULL,
  PRIMARY KEY (`IdUsuario`, `IdEvento`),
  FOREIGN KEY (`IdUsuario`) REFERENCES `usuarios` (`IdUsuario`) ON DELETE CASCADE,
  FOREIGN KEY (`IdEvento`) REFERENCES `eventos` (`IdEvento`) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_spanish_ci;
````


## 4. Creación de Usuarios

### 4.1. Creación de Usuario ***Administrador***

```sql
 INSERT INTO usuarios (
  Nombre, Apellidos, Username, Email, Password, Telefono, FechaNacimiento, Rol, Localidad, Provincia, Avatar
) VALUES (
'Administrador', 'Admin', 'Admin', 'adminhobby@gmail.com', '81dc9bdb52d04dc20036dbd8313ed055', '000000000', '1994-03-26', 'Admin', 'Mérida', 'Badajoz', 'admin.png'
);
```
### 4.2 Insert de ***Categor&iacute;as***

```sql
INSERT INTO categorias (Nombre, Imagen) VALUES
('Deportes', 'deportes.png'),
('Juegos de mesa', 'juegosdemesa.png'),
('Videojuegos', 'videojuegos.png'),
('Lectura y literatura', 'lecturayliteratura.png'),
('Teatro y Cine', 'teatroycine.png'),
('Música y Danza', 'músicaydanza.png'),
('Eventos y Ferias', 'eventosyferias.png'),
('Creatividad y Manualidades', 'creatividadymanualidades.png'),
('Naturaleza y Bienestar', 'naturalezaybienestar.png'),
('Conocimiento y Desarrollo Personal', 'conocimientoydesarrollopersonal.png'),
('Moda y Estilo', 'modayestilo.png'),
('Coleccionismo', 'coleccionismo.png'),
('Tecnología', 'tecnologia.svg'),
('Turismo', 'turismo.svg'),
('Cocina y Gastronomía', 'cocinaygastronomia.svg');
```

### 4.2 Insert de ***Subcategor&iacute;as***

```sql
INSERT INTO subcategorias (IdCategoria, Nombre) VALUES
-- Deportes (1)
(1, 'Fútbol sala'),
(1, 'Tenis'),
(1, 'Pádel'),
(1, 'Baloncesto'),
(1, 'Ciclismo'),
(1, 'Running'),
(1, 'Senderismo'),
(1, 'Gimnasio'),
(1, 'Skateboarding'),
(1, 'Artes marciales'),
-- Juegos de mesa (2)
(2, 'Ajedrez'),
(2, 'Magic: The Gathering'),
(2, 'Warhammer 40K'),
(2, 'Juegos de rol'),
(2, 'Catan'),
(2, 'Dixit'),
(2, 'Intercambio de cartas'),
-- Videojuegos (3)
(3, 'Torneos presenciales'),
(3, 'Cooperativo'),
(3, 'Competitivo'),
(3, 'Streaming'),
(3, 'Retro gaming'),
(3, 'Pokémon GO'),
-- Lectura y literatura (4)
(4, 'Club de lectura'),
(4, 'Lectura conjunta'),
(4, 'Firmas de libros'),
(4, 'Talleres de escritura'),
(4, 'Encuentros con autores'),
-- Teatro y Cine (5)
(5, 'Cine'),
(5, 'Teatro'),
(5, 'Musicales'),
(5, 'Cine al aire libre'),
(5, 'Talleres de actuación'),
-- Música y Danza (6)
(6, 'Conciertos'),
(6, 'Clases de baile'),
(6, 'Ópera'),
(6, 'Ballet'),
(6, 'Música folclórica'),
-- Eventos y Ferias (7)
(7, 'Ferias del libro'),
(7, 'Festivales de arte'),
(7, 'Mercados medievales'),
(7, 'Cosplay'),
(7, 'Eventos culturales'),
-- Creatividad y Manualidades (8)
(8, 'Pintura'),
(8, 'Dibujo'),
(8, 'Fotografía'),
(8, 'Modelismo'),
(8, 'Cerámica'),
(8, 'Lettering'),
(8, 'Scrapbooking'),
-- Naturaleza y Bienestar (9)
(9, 'Jardinería'),
(9, 'Senderismo'),
(9, 'Meditación'),
(9, 'Yoga'),
(9, 'Observación de aves'),
(9, 'Acampada'),
-- Conocimiento y Desarrollo Personal (10)
(10, 'Aprender idiomas'),
(10, 'Club de debate'),
(10, 'Ciencia y tecnología'),
(10, 'Historia'),
(10, 'Escritura creativa'),
-- Moda y Estilo (11)
(11, 'Costura'),
(11, 'Tejido'),
(11, 'Maquillaje'),
(11, 'Customización de ropa'),
-- Coleccionismo (12)
(12, 'Figuras'),
(12, 'Sellos'),
(12, 'Monedas'),
(12, 'Cartas coleccionables'),
(12, 'Colecciones temáticas');
```

### 4.2 Insert de ***Eventos***

```sql
INSERT INTO eventos (Titulo, Descripcion, FechaCreacion, FechaInicio, FechaFin, Creador, Subcategoria, NumParticipantes, Direccion, Localidad, Provincia, ModoEvento, Estado) VALUES
-- Lectura
('Club de lectura mensual', 'Lectura compartida de una novela clásica cada mes.', '2025-05-07', '2025-06-01', '2025-08-01', 3, 34, 12, 'Biblioteca Central, Sala 3', 'Cáceres', 'Cáceres', 'Comunitario', 'Por_Empezar'),
('Taller de escritura creativa', 'Explora técnicas narrativas y crea tus propios relatos.', '2025-05-07', '2025-06-05', '2025-07-10', 2, 37, 15, 'Casa de Cultura, Aula 2', 'Plasencia', 'Cáceres', 'Comunitario', 'Por_Empezar'),

-- Teatro y cine
('Noche de cortometrajes', 'Proyección y debate de cortos independientes.', '2025-05-07', '2025-06-10', '2025-06-10', 3, 42, 30, 'Centro Cultural El Brocense', 'Cáceres', 'Cáceres', 'Comunitario', 'Por_Empezar'),
('Taller de iniciación al teatro', 'Dinámicas para perder el miedo escénico y desarrollar habilidades actorales.', '2025-05-07', '2025-06-15', '2025-07-20', 2, 43, 20, 'Espacio para la Creación Joven', 'Navalmoral de la Mata', 'Cáceres', 'Comunitario', 'Por_Empezar'),
-- Turismo
('Ruta por el casco histórico', 'Recorrido guiado por los puntos clave del patrimonio de la ciudad.', '2025-05-07', '2025-06-08', '2025-06-08', 3, 114, 25, 'Plaza Mayor', 'Trujillo', 'Cáceres', 'Comunitario', 'Por_Empezar'),
('Visita a exposición contemporánea', 'Análisis colectivo de obras de arte moderno en galería local.', '2025-05-07', '2025-06-12', '2025-06-12', 2, 113, 20, 'Galería Arte XXI', 'Cáceres', 'Cáceres', 'Comunitario', 'Por_Empezar'),
-- Música y danza
('Jam session abierta', 'Ven con tu instrumento o voz a improvisar con otros músicos.', '2025-05-07', '2025-06-20', '2025-06-20', 3, 51, 30, 'Sala Boogaloo', 'Cáceres', 'Cáceres', 'Comunitario', 'Por_Empezar'),
('Taller de bailes latinos', 'Aprende los pasos básicos de salsa, bachata y merengue.', '2025-05-07', '2025-06-18', '2025-07-30', 2, 47, 20, 'Academia Ritmo Tropical', 'Plasencia', 'Cáceres', 'Comunitario', 'Por_Empezar'),
-- Eventos y ferias
('Feria medieval local', 'Puestos, representaciones y música ambientada en la Edad Media.', '2025-05-07', '2025-08-01', '2025-08-03', 1, 62, 100, 'Casco Antiguo', 'Cáceres', 'Cáceres', 'Comunitario', 'Por_Empezar'),
('Encuentro cosplay y cultura friki', 'Ven disfrazado de tu personaje favorito y participa en concursos.', '2025-05-07', '2025-07-15', '2025-07-15', 2, 57, 50, 'Palacio de Congresos', 'Cáceres', 'Cáceres', 'Comunitario', 'Por_Empezar');

INSERT INTO eventos (Titulo, Descripcion, FechaCreacion, FechaInicio, FechaFin, Creador, Subcategoria, NumParticipantes, Direccion, Localidad, Provincia, ModoEvento, Estado) VALUES
('Charla de teatro', 'Plan sin presiones para disfrutar juntos de teatro. ¡Te esperamos!', '2025-05-04', '2025-05-04', '2025-05-05', 3, 2, 12, 'Calle Jardín, 32', 'Leganés', 'Madrid', 'Comunitario', 'Por_Empezar'),
('Charla de ciencia', 'Una oportunidad perfecta para compartir nuestra pasión por ciencia. ¡Te esperamos!', '2025-04-26', '2025-04-26', '2025-04-27', 3, 2, 3, 'Avenida del Sol, 50', 'Zaragoza', 'Zaragoza', 'Comunitario', 'Por_Empezar'),
('Taller de manualidades', 'Plan sin presiones para disfrutar juntos de manualidades. ¡Te esperamos!', '2025-04-24', '2025-04-24', '2025-04-25', 2, 3, 4, 'Avenida del Sol, 94', 'Leganés', 'Madrid', 'Comunitario', 'Por_Empezar'),
('Taller de lectura', 'Acércate y disfruta de una experiencia sobre lectura. ¡Te esperamos!', '2025-05-18', '2025-05-18', '2025-05-19', 3, 3, 1, 'Calle Mayor, 55', 'Mataró', 'Barcelona', 'Comunitario', 'Por_Empezar'),
('Evento especial:  tecnología', 'Un encuentro relajado para hablar y explorar tecnología. ¡Te esperamos!', '2025-04-24', '2025-04-24', '2025-04-25', 3, 16, 5, 'Calle Jardín, 74', 'A Coruña', 'A Coruña', 'Comunitario', 'Por_Empezar'),
('Iniciación a música en vivo', 'Si te llama la atención el mundo de música en vivo. ¡Te esperamos!', '2025-04-27', '2025-04-27', '2025-04-28', 3, 16, 2, 'Calle Nueva, 24', 'A Coruña', 'A Coruña', 'Comunitario', 'Por_Empezar'),
('Iniciación a música en vivo', 'Actividad ideal para quienes se interesan por música en vivo. ¡Te esperamos!', '2025-05-08', '2025-05-08', '2025-05-09', 2, 17, 12, 'Avenida del Sol, 113', 'Utebo', 'Zaragoza', 'Comunitario', 'Por_Empezar'),
('Conoce más de gastronomía', 'Un encuentro relajado para hablar y explorar gastronomía. ¡Te esperamos!', '2025-05-03', '2025-05-03', '2025-05-04', 2, 17, 4, 'Calle Nueva, 97', 'Plasencia', 'Cáceres', 'Comunitario', 'Por_Empezar'),
('Actividad sobre ajedrez', 'Acércate y disfruta de una experiencia sobre ajedrez. ¡Te esperamos!', '2025-04-07', '2025-04-07', '2025-04-08', 2, 27, 6, 'Plaza de España, 85', 'Plasencia', 'Cáceres', 'Comunitario', 'Por_Empezar'),
('Descubre tecnología', 'Una oportunidad perfecta para compartir nuestra pasión por tecnología. ¡Te esperamos!', '2025-05-14', '2025-05-14', '2025-05-15', 3, 27, 5, 'Calle Nueva, 16', 'Getafe', 'Madrid', 'Comunitario', 'Por_Empezar'),
('Iniciación a historia', 'Plan sin presiones para disfrutar juntos de historia. ¡Te esperamos!', '2025-05-28', '2025-05-28', '2025-05-29', 3, 28, 9, 'Calle Nueva, 56', 'Getafe', 'Madrid', 'Comunitario', 'Por_Empezar'),
('Explorando gastronomía', 'Plan sin presiones para disfrutar juntos de gastronomía. ¡Te esperamos!', '2025-04-26', '2025-04-26', '2025-04-27', 2, 28, 7, 'Plaza de España, 76', 'Sevilla', 'Sevilla', 'Comunitario', 'Por_Empezar'),
('Descubre manualidades', 'Nos reuniremos para aprender y disfrutar sobre manualidades. ¡Te esperamos!', '2025-05-27', '2025-05-27', '2025-05-28', 3, 35, 7, 'Avenida del Sol, 53', 'Utebo', 'Zaragoza', 'Comunitario', 'Por_Empezar'),
('Charla de manualidades', 'Plan sin presiones para disfrutar juntos de manualidades. ¡Te esperamos!', '2025-05-27', '2025-05-27', '2025-05-28', 2, 35, 6, 'Plaza de España, 3', 'Barcelona', 'Barcelona', 'Comunitario', 'Por_Empezar'),
('Iniciación a baile', 'Si te llama la atención el mundo de baile. ¡Te esperamos!', '2025-05-17', '2025-05-17', '2025-05-18', 2, 66, 5, 'Calle Mayor, 101', 'A Coruña', 'A Coruña', 'Comunitario', 'Por_Empezar'),
('Iniciación a baile', 'Nos reuniremos para aprender y disfrutar sobre baile. ¡Te esperamos!', '2025-04-06', '2025-04-06', '2025-04-07', 2, 66, 3, 'Avenida del Sol, 101', 'Torrent', 'Valencia', 'Comunitario', 'Por_Empezar'),
('Charla de ciencia', 'Si te llama la atención el mundo de ciencia. ¡Te esperamos!', '2025-05-02', '2025-05-02', '2025-05-03', 3, 70, 9, 'Calle Nueva, 64', 'Cáceres', 'Cáceres', 'Comunitario', 'Por_Empezar'),
('Iniciación a cine', 'Si te llama la atención el mundo de cine. ¡Te esperamos!', '2025-05-23', '2025-05-23', '2025-05-24', 2, 70, 9, 'Calle Jardín, 26', 'Zaragoza', 'Zaragoza', 'Comunitario', 'Por_Empezar'),
('Taller de ajedrez', 'Un encuentro relajado para hablar y explorar ajedrez. ¡Te esperamos!', '2025-04-28', '2025-04-28', '2025-04-29', 2, 74, 7, 'Calle Nueva, 109', 'Zaragoza', 'Zaragoza', 'Comunitario', 'Por_Empezar'),
('Actividad sobre cine', 'Una oportunidad perfecta para compartir nuestra pasión por cine. ¡Te esperamos!', '2025-04-25', '2025-04-25', '2025-04-26', 2, 74, 5, 'Plaza de España, 51', 'Getafe', 'Madrid', 'Comunitario', 'Por_Empezar'),
('Conoce más de gastronomía', 'Una oportunidad perfecta para compartir nuestra pasión por gastronomía. ¡Te esperamos!', '2025-04-09', '2025-04-09', '2025-04-10', 2, 75, 11, 'Calle Mayor, 93', 'Mérida', 'Badajoz', 'Comunitario', 'Por_Empezar'),
('Sesión abierta de tecnología', 'Nos reuniremos para aprender y disfrutar sobre tecnología. ¡Te esperamos!', '2025-04-01', '2025-04-01', '2025-04-02', 2, 75, 4, 'Avenida del Sol, 72', 'Leganés', 'Madrid', 'Comunitario', 'Por_Empezar'),
('Charla de ciencia', 'Plan sin presiones para disfrutar juntos de ciencia. ¡Te esperamos!', '2025-04-08', '2025-04-08', '2025-04-09', 3, 81, 12, 'Plaza de España, 39', 'Badajoz', 'Badajoz', 'Comunitario', 'Por_Empezar'),
('Descubre senderismo', 'Plan sin presiones para disfrutar juntos de senderismo. ¡Te esperamos!', '2025-05-12', '2025-05-12', '2025-05-13', 2, 81, 11, 'Plaza de España, 21', 'Torrent', 'Valencia', 'Comunitario', 'Por_Empezar'),
('Explorando fotografía', 'Plan sin presiones para disfrutar juntos de fotografía. ¡Te esperamos!', '2025-05-23', '2025-05-23', '2025-05-24', 3, 84, 1, 'Calle Jardín, 102', 'Mérida', 'Badajoz', 'Comunitario', 'Por_Empezar'),
('Sesión abierta de música en vivo', 'Plan sin presiones para disfrutar juntos de música en vivo. ¡Te esperamos!', '2025-04-30', '2025-04-30', '2025-05-01', 3, 84, 6, 'Avenida del Sol, 100', 'Getafe', 'Madrid', 'Comunitario', 'Por_Empezar'),
('Quedada de manualidades', 'Actividad ideal para quienes se interesan por manualidades. ¡Te esperamos!', '2025-05-12', '2025-05-12', '2025-05-13', 3, 91, 4, 'Calle Jardín, 46', 'A Coruña', 'A Coruña', 'Comunitario', 'Por_Empezar'),
('Conoce más de videojuegos', 'Sesión participativa donde profundizaremos en videojuegos. ¡Te esperamos!', '2025-05-23', '2025-05-23', '2025-05-24', 3, 91, 8, 'Plaza de España, 16', 'Motril', 'Granada', 'Comunitario', 'Por_Empezar'),
('Iniciación a conversación', 'Sesión participativa donde profundizaremos en conversación. ¡Te esperamos!', '2025-04-12', '2025-04-12', '2025-04-13', 2, 96, 10, 'Calle Mayor, 2', 'Ferrol', 'A Coruña', 'Comunitario', 'Por_Empezar'),
('Quedada de senderismo', 'Plan sin presiones para disfrutar juntos de senderismo. ¡Te esperamos!', '2025-05-13', '2025-05-13', '2025-05-14', 2, 96, 6, 'Calle Mayor, 19', 'Torrent', 'Valencia', 'Comunitario', 'Por_Empezar'),
('Conoce más de escritura', 'Un encuentro relajado para hablar y explorar escritura. ¡Te esperamos!', '2025-05-25', '2025-05-25', '2025-05-26', 2, 98, 6, 'Plaza de España, 30', 'Mataró', 'Barcelona', 'Comunitario', 'Por_Empezar'),
('Explorando cómics', 'Plan sin presiones para disfrutar juntos de cómics. ¡Te esperamos!', '2025-05-27', '2025-05-27', '2025-05-28', 3, 98, 11, 'Avenida del Sol, 31', 'Dos Hermanas', 'Sevilla', 'Comunitario', 'Por_Empezar'),
('Charla de cómics', 'Plan sin presiones para disfrutar juntos de cómics. ¡Te esperamos!', '2025-04-29', '2025-04-29', '2025-04-30', 3, 103, 9, 'Avenida del Sol, 88', 'Mérida', 'Badajoz', 'Comunitario', 'Por_Empezar'),
('Evento especial:  manualidades', 'Si te llama la atención el mundo de manualidades. ¡Te esperamos!', '2025-04-03', '2025-04-03', '2025-04-04', 3, 103, 9, 'Plaza de España, 49', 'Mataró', 'Barcelona', 'Comunitario', 'Por_Empezar'),
('Evento especial:  escritura', 'Sesión participativa donde profundizaremos en escritura. ¡Te esperamos!', '2025-04-30', '2025-04-30', '2025-05-01', 3, 105, 9, 'Calle Jardín, 58', 'Ferrol', 'A Coruña', 'Comunitario', 'Por_Empezar'),
('Actividad sobre artesanía', 'Plan sin presiones para disfrutar juntos de artesanía. ¡Te esperamos!', '2025-05-06', '2025-05-06', '2025-05-07', 3, 105, 2, 'Plaza de España, 111', 'Valencia', 'Valencia', 'Comunitario', 'Por_Empezar'),
('Sesión abierta de ciencia', 'Plan sin presiones para disfrutar juntos de ciencia. ¡Te esperamos!', '2025-04-21', '2025-04-21', '2025-04-22', 2, 108, 11, 'Avenida del Sol, 85', 'Valencia', 'Valencia', 'Comunitario', 'Por_Empezar'),
('Iniciación a baile', 'Una oportunidad perfecta para compartir nuestra pasión por baile. ¡Te esperamos!', '2025-04-04', '2025-04-04', '2025-04-05', 3, 108, 11, 'Calle Nueva, 36', 'Badajoz', 'Badajoz', 'Comunitario', 'Por_Empezar'),
('Conoce más de artesanía', 'Actividad ideal para quienes se interesan por artesanía. ¡Te esperamos!', '2025-05-14', '2025-05-14', '2025-05-15', 2, 117, 5, 'Avenida del Sol, 104', 'Utebo', 'Zaragoza', 'Comunitario', 'Por_Empezar'),
('Actividad sobre debate', 'Un encuentro relajado para hablar y explorar debate. ¡Te esperamos!', '2025-05-06', '2025-05-06', '2025-05-07', 2, 117, 9, 'Avenida del Sol, 101', 'Ferrol', 'A Coruña', 'Comunitario', 'Por_Empezar'),
('Charla de viajes', 'Actividad ideal para quienes se interesan por viajes. ¡Te esperamos!', '2025-05-06', '2025-05-06', '2025-05-07', 3, 118, 4, 'Plaza de España, 90', 'Badajoz', 'Badajoz', 'Comunitario', 'Por_Empezar'),
('Charla de ciencia', 'Plan sin presiones para disfrutar juntos de ciencia. ¡Te esperamos!', '2025-05-06', '2025-05-06', '2025-05-07', 2, 118, 10, 'Calle Jardín, 84', 'Mataró', 'Barcelona', 'Comunitario', 'Por_Empezar'),
('Descubre cine', 'Actividad ideal para quienes se interesan por cine. ¡Te esperamos!', '2025-05-19', '2025-05-19', '2025-05-20', 2, 119, 8, 'Avenida del Sol, 5', 'Barcelona', 'Barcelona', 'Comunitario', 'Por_Empezar'),
('Evento especial:  historia', 'Un encuentro relajado para hablar y explorar historia. ¡Te esperamos!', '2025-05-09', '2025-05-09', '2025-05-10', 2, 119, 9, 'Calle Nueva, 23', 'Mérida', 'Badajoz', 'Comunitario', 'Por_Empezar');
```
