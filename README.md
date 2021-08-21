# BookStore-Laboratorio

**Curso:** ST0255 Telemática. <br />
**Título:** Desplegando una Web App considerando Front y Back end. <br />
**Objetivo:** Desarrollar habilidades que permita el desplegar una aplicación web teniendo en cuenta una arquitectura cliente/servidor así como de “N” capas (layer) (presentación/lógica de negocio/persistencia de datos) distribuida en diferentes máquinas.  <br />

**Duración:** 45 mins.

## 1. Introducción
En la actualidad el despliegue de las aplicaciones es una parte fundamental para el éxito de las organizaciones. Igualmente, no se puede negar que, muchas de las aplicaciones se desarrollan considerando una vista web.  Es por esta razón, que entender los elementos que componen una aplicación web (el cliente así como servidor), el protocolo (http) que soporta la comunicación entre los elementos así como la arquitectura, tanto a nivel de software como de despliegue, es un aspecto fundamental para el proceso de formación en el área de la computación. 

En este laboratorio, se desarrollaran las habilidades necesarias para el despliegue de una aplicación web que considera una arquitectura de 3 capas (presentación/lógica de negocio/persistencia de datos). 

## 2. Recursos
Para el desarrollo de este laboratorio se requiere una cuenta en AWS que le permita desplegar diferentes instancias EC2 para instalar sistema operativo Amazon Machine Image (AMI). 

## 3. Descripción de la Aplicación Web
El proyecto a desplegar en este laboratorio es una aplicación web. La aplicación permite visualizar una colección de recursos, para efectos de este caso, libros. Igualmente, cuando el usuario selecciona alguno de los recursos, se ofrece una vista con información detallada sobre el recurso seleccionado. La información de los recursos (libros) se encuentra almacenada en base de datos. La aplicación tiene tres (vistas): raíz (“/”, home), descripción  detallada de los recursos libros y acerca de. 

![Figura 1](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/Figura1.png) <br />
*Figura 1. Vista del home de la aplicación.* <br />

![Figura 2](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/Figura2.png) <br />
*Figura 2. Vista detallada para un objeto libro.* <br />

![Figura 3](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/Figura3.png) <br />
*Figura 3. Vista detallada Acerca de.* <br />

### 3.1 Arquitectura de la aplicación
Es una aplicación web la cual emplea un estilo arquitectónico de división en capas. Para efectos de este proyecto se definió una arquitectura de dos (3) capas. Capa de presentación, lógica de negocio y persistencia de datos. Este es un estilo arquitectónico que permite que cada capa se ejecute sobre su propia infraestructura. De igual forma, es posible que un equipo de desarrollo se concentre en cada capa. 

A continuación se ofrece una descripción de la aplicación para cada una de las capas   
•	**Descripción de capa de presentación (Front End):** Esta capa se encarga de todos los aspectos relacionados con la interfaz de usuario. A esta capa se accede a través del browser. Igualmente, se encarga de la comunicación con el back end, en este caso, utilizando una API REST. Particularmente en este laboratorio, la capa de presentación o front end se encuentra desarrollado utilizando React. Ésta se define como una librería de java script para desarrollar la capa de presentación. En este sentido, la principal función de react es renderizar código html en el browser.  Para efectos del manejo de estilos (CSS), se empleo react-boostrap 

•	**Descripción del Back End:** En este estilo arquitectónico, esta es la capa de la mitad en la cual se ejecuta y lleva a cabo la lógica de negocio. El back end se encuentra desarrollado empleando tecnología de scripting del lado del servidor, para este caso node.js. Igualmente utilizamos un framework de desarrollo de aplicaciones web denominado express así como mongoose para la conexión con la bases de datos.

•	**Descripción de la persistencia de datos:** En esta capa es donde la información es gestionada y almacenada. En este laboratorio, los datos se almacenan en un motor de bases de datos orientado a documentos, para efectos de esta aplicación Mongo DB. Particularmente, estaremos utilizando Mongo DB, el cual es un servicio de bases de datos tipo NO SQL de forma local. 

En el siguiente diagrama se puede observar el flujo principal que se requieren implementar para el manejo de las peticiones http. 

El módulo “server.js” inicializa el proceso servidor en el puerto 5000, establece la conexión con la base de datos y, una vez recibe las peticiones http, selecciona y usa el módulo de ruta (bookRoute.js) adecuado para el procesamiento de la petición http entrante. Aquí, se envía la información al controlador apropiado (“bookControler”) para que este obtenga los datos que se solicitan desde el front end a través del model (“bookModels.js”). En este caso lo que se envía de respuesta es un Java Script Object Notation (JSON) hacia el front end. El modelo se encarga de obtener los datos solicitados de la base de datos.


## 4. Estructura del proyecto
El proyecto se encuentra estructurado en dos grandes carpetas: frontend y backend. En la imagen se puede encontrar la estructura así como los diferentes folders que componen el proyecto.
![Directorios](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/Directorios.png) <br />
*Figura . Estructura de directorios.*


## 5. Configuración de base de datos: MongoDB

Tutorial [https://docs.mongodb.com/manual/tutorial/install-mongodb-on-amazon/]

Code block
$ sudo nano /etc/yum.repos.d/mongodb-org-5.0.repo
[mongodb-org-5.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/amazon/2/mongodb-org/5.0/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-5.0.asc

$ sudo systemctl start mongod
$ sudo systemctl status mongod
$ mongosh
$ use bookstore
$ db.user.insert({name: "...", author: "..."})
