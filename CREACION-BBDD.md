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
  PRIMARY KEY (`IdCategoria`),
  UNIQUE (`Nombre`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_spanish_ci;
```

### 3.2. Creación Tabla ***usuarios***

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
  `Avatar` varchar(30) COLLATE utf8_spanish_ci NOT NULL DEFAULT 'avatar.png',
  PRIMARY KEY (`IdUsuario`),
  UNIQUE (`Email`),
  UNIQUE (`Username`),
  UNIQUE (`Telefono`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_spanish_ci;
```

### 3.3. Creación Tabla ***eventos***

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

### 3.3. Creación Tabla ***usuarioeventos***

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
