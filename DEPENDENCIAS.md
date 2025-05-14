# Dependencias utilizadas en la aplicaci&oacute;n

## &Iacute;ndice de dependencias

1. [Java EE Web API](#1-java-ee-web-api)  
2. [JSTL](#2-jstl)  
3. [Commons BeanUtils](#3-commons-beanutils)  
4. [MySQL Connector/J](#4-mysql-connectorj)  
5. [Hibernate Core](#5-hibernate-core)  
6. [org.json](#6-orgjson)  
7. [Gson](#7-gson)  
8. [Jakarta Mail](#8-jakarta-mail)  

---

## 1. Java EE Web API

```java
<dependency>
    <groupId>javax</groupId>
    <artifactId>javaee-web-api</artifactId>
    <version>7.0</version>
    <scope>provided</scope>
</dependency>
```
>[!NOTE]
> Esta dependencia incluye todas las APIs cl&aacute;sicas de Java para el desarrollo web (servlets, JSP, etc.).

---

## JSTL

```java
<dependency>
    <groupId>jstl</groupId>
    <artifactId>jstl</artifactId>
    <version>1.2</version>
</dependency>
```
>[!NOTE]
> Nos permite usar etiquetas pr&aacute;cticas en JSP como bucles o condicionales sin meter Java puro en el HTML. B&aacute;sicamente hace que las JSP sean m&aacute;s limpias y f&aacute;ciles de leer.

---

## Commons BeanUtils

```java
<dependency>
    <groupId>commons-beanutils</groupId>
    <artifactId>commons-beanutils</artifactId>
    <version>1.9.4</version>
</dependency>
```
>[!NOTE]
> Esta librer&iacute;a de Apache sirve para copiar propiedades entre objetos Java (beans) de forma autom&aacute;tica. Viene genial cuando tienes formularios y necesitas pasar datos r&aacute;pido de un lado a otro sin escribir mil getters y setters.

---

## MySQL Connector/J

```java
<dependency>
    <groupId>com.mysql</groupId>
    <artifactId>mysql-connector-j</artifactId>
    <version>8.3.0</version>
</dependency>
```
>[!NOTE]
> Es el conector oficial de MySQL. Sirve principalmente para que una app de Java pueda comunicarse con la base de datos MySQL.

---

## Hibernate Core

```java
<dependency>
    <groupId>org.hibernate</groupId>
    <artifactId>hibernate-core</artifactId>
    <version>5.4.10.Final</version>
</dependency>
```
>[!NOTE]
> Una de las librerías m&aacute;s conocidas para mapear clases Java con tablas de bases de datos. Sirve para trabajar directamente con objetos.

---

## org.json

```java
<dependency>
    <groupId>org.json</groupId>
    <artifactId>json</artifactId>
    <version>20231013</version>
</dependency>
```
>[!NOTE]
> Librer&iacute;a de Google para convertir objetos Java a JSON y viceversa. S&uacute;per &uacute;til para enviar y recibir datos en aplicaciones web o APIs REST.

---

## Jakarta Mail

```java
<dependency>
    <groupId>com.sun.mail</groupId>
    <artifactId>jakarta.mail</artifactId>
    <version>2.0.1</version>
</dependency>
```
>[!NOTE]
> Te permite enviar correos desde tu aplicaci&oacute;n Java. Ideal para notificaciones, confirmaciones de registro, recuperaci&oacute;n de contrase&ntilde;as, etc.

---

## ℹ️ Informaci&oacute;n del proyecto:

🧑‍💻**Alumno:** *Alberto Miguel S&aacute;nchez Mac&iacute;as*

🌐**Aplicaci&oacute;n:** *EntreHobbies*

🧑‍🏫**Tutor FCT:** *Francisco Mera Calder&oacute;n*

🏫**Instituto:** *IES Albarregas*

🏫**Clase:** *DAW-2B* 
