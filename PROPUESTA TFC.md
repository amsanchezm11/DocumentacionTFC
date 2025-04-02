# DocumentacionTFC - Comparte tu Hobby
Propuesta del proyecto final 2025

**Alumno:** *Alberto M. S&aacute;nchez Mac&iacute;as* <br>
**Fecha:** *25/03/2025*

# Índice

1. [Título y descripción general del proyecto](#título-y-descripción-general-del-proyecto)
2. [Identificación del proyecto](#identificación-del-proyecto)
3. [Justificación y objetivos](#justificación-y-objetivos)
4. [Contenidos y aspectos principales](#contenidos-y-aspectos-principales)
5. [Medios que se utilizarán](#medios-que-se-utilizarán)
6. [Áreas del ciclo formativo](#áreas-del-ciclo-formativo)


## Título y descripción general del proyecto

***Comparte tu Hobby*** – Plataforma para la organización de eventos según intereses personales. 

 ***"Comparte tu Hobby"*** es una plataforma web que permite a los usuarios crear y unirse a eventos según sus intereses, como deportes, juegos de mesa, videojuegos, cultura, música y más. Los eventos se pueden filtrar por categoría y localidad, y se clasifican en abiertos, privados y competitivos. Cada usuario tendrá un perfil con su alias, avatar, hobbies y otros datos adicionales. El objetivo es facilitar la conexión entre personas con aficiones similares y fomentar la participación en actividades sociales. 

## Identificación del proyecto

**Participante:** Alberto Miguel Sánchez Macías 

**Ciclo formativo:** Desarrollo de Aplicaciones Web 

**Centro educativo:** IES Albarregas, Mérida. 

## Justificación y objetivos

### Justificación:
El proyecto **Comparte tu Hobby** surge porque actualmente no hay una plataforma bien estructurada donde la gente pueda encontrar y organizar eventos según sus aficiones. La mayoría de las veces, las personas dependen de grupos en redes sociales o aplicaciones genéricas, lo que hace que sea complicado descubrir actividades interesantes o conectar con gente que comparta los mismos gustos.

Además, en muchas ciudades y pueblos hay personas que quieren organizar eventos, pero no tienen una forma sencilla de hacerlo o de llegar a más gente interesada. Con esta aplicación, se busca crear un espacio donde cualquiera pueda publicar eventos o apuntarse a los que ya existen, facilitando la organización y la participación en actividades de todo tipo.

### ¿Qué problemas soluciona este proyecto?

● **Es difícil encontrar eventos específicos** → La aplicación tendrá filtros por categoría y ubicación para que sea más fácil buscar eventos.  

● **No hay una plataforma dedicada a la gestión de eventos por hobbies** → Aquí los usuarios podrán crear, modificar y gestionar eventos de manera sencilla.  

● **A veces es complicado organizar actividades grupales** → Habrá distintos tipos de eventos (abiertos, privados y competitivos) para adaptarse a diferentes necesidades.  

● **Las personas que organizan eventos no siempre son reconocidas** → Se añadirá una insignia de "Organizador" para destacar a quienes crean eventos con frecuencia.  

### ¿Qué mejoras traerá la aplicación?

● **Búsqueda rápida y sencilla** con filtros para encontrar eventos por tipo y ubicación.  

● **Un sistema claro para apuntarse a eventos** sin necesidad de estar en mil grupos de redes sociales.  

● **Perfiles personalizados** donde los usuarios podrán mostrar los hobbies que practican habitualmente e incluso los nuevos hobbies en los que está interesado introducirse.  

● **Un espacio para conectar con gente** con los mismos intereses, creando una comunidad activa en torno a cada afición. 

El objetivo principal es que la gente pueda descubrir y participar en actividades de manera sencilla, sin complicaciones y con un sistema bien organizado.

## Contenidos y aspectos principales

### Requisitos Funcionales (¿Qué podrá hacer la aplicación?)

La aplicación permitirá a los usuarios:

1. **Registrarse y gestionar su perfil**
   - Crear un perfil con alias, avatar (obligatorio), contraseña, localidad y hobbies.
   - Editar su información.

2. **Crear y gestionar eventos**
   - Publicar eventos especificando nombre, categoría, tipo, ubicación, fecha y descripción.
   - Modificar o eliminar eventos creados.

3. **Buscar y unirse a eventos**
   - Filtros por categoría, ubicación y palabras clave.
   - Solicitar unirse a eventos competitivos o privados.
   - Inscribirse directamente en eventos abiertos.

4. **Interacción entre usuarios**
   - Ver perfiles de otros usuarios y sus eventos organizados o en los que han participado.
   - Obtener una insignia de "Organizador" si se crean eventos con frecuencia y son bien valorados.

### Requisitos No Funcionales (Aspectos técnicos y de rendimiento)

● **Interfaz intuitiva y accesible**: La aplicación debe ser fácil de usar, con un diseño atractivo y adaptable a distintos tamaños de pantalla.  

● **Seguridad y privacidad**: Protección de datos personales y sistema de autenticación seguro.  

● **Escalabilidad**: La aplicación debe ser capaz de soportar un aumento en el número de usuarios y eventos sin afectar el rendimiento.  

● **Tiempo de respuesta óptimo**: Las búsquedas y la carga de eventos deben ser rápidas.  

● **Compatibilidad**: La aplicación debe ser accesible desde distintos navegadores y dispositivos.  


## Medios que se utilizarán

### Sistema Operativo:
- **Windows 11 Home**, 8 GB de RAM y 250 GB de memoria.

### Lenguajes de programación:
- **Backend** → Java 11  
- **Frontend** → JavaScript + JSP y JSTL  
- **Bases de datos** → MySQL 8.0

### Frameworks:
- **Hibernate 5** → Para la gestión de bases de datos mediante ORM.  
- **Bootstrap 5** → Para el diseño de la interfaz web.  
- **JSP y JSTL** → Para la generación de contenido dinámico en el frontend.

### Entorno de desarrollo:
(Aún por determinar) Se están contemplando dos opciones de IDE para desarrollar la aplicación. Una es **NetBeans 19** y la otra es **IntelliJ IDEA 2023.3.4**. Ambos contarán con **JDK11** y **Java EE 7**. En un principio, el IDE elegido es **NetBeans 19**, pero no se descarta la posibilidad de cambiar a **IntelliJ** en un futuro por mayor agilidad de desarrollo para el proyecto.

### Control de versiones:
- **GitHub** → Se utilizará la aplicación de escritorio **GitHub Desktop**.

### Servidor de aplicaciones:
- **Apache Tomcat 8**

### Despliegue:
De momento, el despliegue de la aplicación se realizará en el servidor del instituto. Queda pendiente consultar alguna opción alternativa con mi tutor **Francisco Mera Calderón**.


## Áreas del ciclo formativo

### Desarrollo Web entorno Servidor:
Abarcar toda la lógica del backend y la gestión de la base de datos, asegurando la correcta comunicación entre el cliente y el servidor.

### Desarrollo Web entorno Cliente:
Implementar validaciones en el frontend para mejorar la experiencia de usuario y evitar errores en la entrada de datos.

### Diseño de interfaces Web:
Para la parte visual y de usabilidad de la aplicación, utilizando **Bootstrap** junto con **CSS** para garantizar un diseño responsivo y atractivo.

### Despliegue de aplicaciones Web:
Configuración y puesta en marcha de la aplicación en un servidor del instituto para pruebas y demostraciones.

