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
('Coleccionismo', 'coleccionismo.png');
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
