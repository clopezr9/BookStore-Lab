# BookStore-Laboratorio

**Curso:** ST0255 Telemática. 
**Título:** Desplegando una Web App considerando Front y Back end. 
**Objetivo:** Desarrollar habilidades que permita el desplegar una aplicación web teniendo en cuenta una arquitectura cliente/servidor así como de “N” capas (layer) (presentación/lógica de negocio/persistencia de datos) distribuida en diferentes máquinas.  

**Duración:** 45 mins.

## 1. Introducción
En la actualidad el despliegue de las aplicaciones es una parte fundamental para el éxito de las organizaciones. Igualmente, no se puede negar que, muchas de las aplicaciones se desarrollan considerando una vista web.  Es por esta razón, que entender los elementos que componen una aplicación web (el cliente así como servidor), el protocolo (http) que soporta la comunicación entre los elementos así como la arquitectura, tanto a nivel de software como de despliegue, es un aspecto fundamental para el proceso de formación en el área de la computación. 

En este laboratorio, se desarrollaran las habilidades necesarias para el despliegue de una aplicación web que considera una arquitectura de 3 capas (presentación/lógica de negocio/persistencia de datos). 

## 2. Recursos
Para el desarrollo de este laboratorio se requiere una cuenta en AWS que le permita desplegar diferentes instancias EC2 para instalar sistema operativo Amazon Machine Image (AMI). 

## 3. Descripción de la Aplicación Web
El proyecto a desplegar en este laboratorio es una aplicación web. La aplicación permite visualizar una colección de recursos, para efectos de este caso, libros. Igualmente, cuando el usuario selecciona alguno de los recursos, se ofrece una vista con información detallada sobre el recurso seleccionado. La información de los recursos (libros) se encuentra almacenada en base de datos. La aplicación tiene tres (vistas): raíz (“/”, home), descripción  detallada de los recursos libros y acerca de. 
![Figura 1](https://github.com/clopezr9/BookStore-Lab/blob/main/Imagenes-Bookstore/Figura1.png) <br />
*Figura 1. Vista del home de la aplicación.* <br />

![Figura 2](https://github.com/clopezr9/BookStore-Lab/blob/main/Imagenes-Bookstore/Figura2.png) <br />
*Figura 2. Vista detallada para un objeto libro.* <br />

![Figura 3](https://github.com/clopezr9/BookStore-Lab/blob/main/Imagenes-Bookstore/Figura3.png) <br />
*Figura 3. Vista detallada Acerca de.* <br />

### 3.1 Arquitectura de la aplicación
Es una aplicación web la cual emplea un estilo arquitectónico de división en capas. Para efectos de este proyecto se definió una arquitectura de dos (3) capas. Capa de presentación, lógica de negocio y persistencia de datos. Este es un estilo arquitectónico que permite que cada capa se ejecute sobre su propia infraestructura. De igual forma, es posible que un equipo de desarrollo se concentre en cada capa. 

A continuación se ofrece una descripción de la aplicación para cada una de las capas   
