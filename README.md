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

![Figura 4](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/Arquitectura-BookStore.png) <br />
*Figura 4. Arquitectura.*<br />
A continuación se ofrece una descripción de la aplicación para cada una de las capas   
•	**Descripción de capa de presentación (Front End):** Esta capa se encarga de todos los aspectos relacionados con la interfaz de usuario. A esta capa se accede a través del browser. Igualmente, se encarga de la comunicación con el back end, en este caso, utilizando una API REST. Particularmente en este laboratorio, la capa de presentación o front end se encuentra desarrollado utilizando React. Ésta se define como una librería de java script para desarrollar la capa de presentación. En este sentido, la principal función de react es renderizar código html en el browser.  Para efectos del manejo de estilos (CSS), se empleo react-boostrap 

•	**Descripción del Back End:** En este estilo arquitectónico, esta es la capa de la mitad en la cual se ejecuta y lleva a cabo la lógica de negocio. El back end se encuentra desarrollado empleando tecnología de scripting del lado del servidor, para este caso node.js. Igualmente utilizamos un framework de desarrollo de aplicaciones web denominado express así como mongoose para la conexión con la bases de datos.

•	**Descripción de la persistencia de datos:** En esta capa es donde la información es gestionada y almacenada. En este laboratorio, los datos se almacenan en un motor de bases de datos orientado a documentos, para efectos de esta aplicación Mongo DB. Particularmente, estaremos utilizando Mongo DB, el cual es un servicio de bases de datos tipo NO SQL de forma local. 

En el siguiente diagrama se puede observar el flujo principal que se requieren implementar para el manejo de las peticiones http. 

![Figura 5](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/Diagrama_de_flujo.PNG) <br />
*Figura 5. Diagrama de flujo*<br />

El módulo “server.js” inicializa el proceso servidor en el puerto 5000, establece la conexión con la base de datos y, una vez recibe las peticiones http, selecciona y usa el módulo de ruta (bookRoute.js) adecuado para el procesamiento de la petición http entrante. Aquí, se envía la información al controlador apropiado (“bookControler”) para que este obtenga los datos que se solicitan desde el front end a través del model (“bookModels.js”). En este caso lo que se envía de respuesta es un Java Script Object Notation (JSON) hacia el front end. El modelo se encarga de obtener los datos solicitados de la base de datos.


## 4. Estructura del proyecto
El proyecto se encuentra estructurado en dos grandes carpetas: frontend y backend. En la imagen se puede encontrar la estructura así como los diferentes folders que componen el proyecto.

![Directorios](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/Directorios.png) <br />
*Figura 6. Estructura de directorios.*

## 5. Despliegue de la aplicación
A continuación se presenta el conjunto de pasos para poder desplegar la aplicación web.

### 5.1. Arquitectura del despliegue
A continuación en la figura, se puede observar la vista de despliegue para la aplicación en AWS.

![Arquitectura de despliegue](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/Arquitectura_del_despliegue.jpg) <br />
*Figura 7. Estructura de directorios.*

Con un poco mas de detalle, en la instancia EC2 seleccionada para desplegar el front end, vamos a utilizar un servidor web nginx para alojar el front end. En este caso vamos a desplegar todo lo relacionado con el front end el directorio raíz que nos permita alojar el contenido html, css e imágenes. Para esto, en el directorio en el que el código fuente desarrollado, debemos seleccionar la carpeta build que se genero anteriormente. En este máquina instalaremos el servidor web nginx para soportar el front end y utilizarlo como reverse proxy con el fin de podernos comunicar con el back end.

### 5.2. Instancie tres (3) máquinas EC2 en la consola de AWS.
Por favor siga los pasos e instrucciones de la guía de laboratorio número dos para realizar este paso.

### 5.3.	Asociando una dirección IP pública elástica:
Para efectos del despliegue de la aplicación, para cada una de las instancias desplegadas vamos a requerir direcciones IP públicas. Recuerde que una dirección IP pública es aquella que es valida en el contexto de Internet. Para efectos de este laboratorio vamos a solicitar un tipo de dirección IP pública en AWS que se denominan direcciones IP elásticas. Una característica de estas direcciones IP es que son estáticas (por esto se quiere decir que no cambian en el tiempo). Esto es importante para el despliegue de una aplicación, dado que si la máquina se cae y se reinicia, se mantiene asociada la misma dirección IP pública, lo cual no afectará la prestación del servicio. Para asociar una dirección IP elástica, siga los siguientes pasos que se describen a continuación:

En el menú de “Red y Seguridad (Network and Security)”, seleccione la opción de IP elásticas

![AWS1](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/AWS1.PNG) <br />

Ahora, escoja la opción de “Allocate Elastic IP Address”.

![AWS2](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/AWS2.PNG) <br />

Una vez se haya asignado la dirección la escogemos y la asociamos a la instancia que designemos para el front end. 

![AWS3](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/AWS3.PNG) <br />

Ahora asocie la IP elástica a la máquina que desee (bien sea front end y back end). 

![AWS4](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/AWS4.PNG) <br />

### 5.4.	Sesión con la EC2 instanciada via SSH.
-	En el menú del servicio EC2, seleccione la instancia con la cual desea establecer la conexión. 

![AWS5](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/AWS5.PNG) <br />

-	Cuando seleccione la opción de conectarse, le aparecerá un cuadro parecido. Tenga presente que debe cambiar los permisos de el archivo key (.pem). 

![AWS6](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/AWS6.PNG) <br />

- En una terminal de consola desde su máquina, inicie una sesión ssh contra el servidor que configuro tal como lo indica la sesión de “example” en la sesión anterior. 
- Como resultado debe haber podido establecer la sesión con la instancia EC2.

![AWS7](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/AWS7.PNG) <br />

### 5.5. Despliegue de Front-End.
Para cada una de las instancias que se desplegaron, actualicemos las aplicaciones que tenemos instaladas en la máquina:
<pre><code> $ sudo yum update </code></pre>

### 5.6. Instalar el servidor web Nginx en el Front End.
Para efectos de este laboratorio, vamos a utilizar un servidor web como Nginx, con el fin de soporta el despliegue de nuestro front end. Por favor, digite el siguiente comando para proceder a instalar el servidor Nginx.
<pre><code> $ sudo amazon-linux-extras install nginx1.12 </code></pre>

Una vez esta instalado vamos a proceder a configurar el servidor. Para esto debemos modificar el archivo de configuración de nginx ubicado en /etc/nginx
<pre><code> $ sudo nano /etc/nginx/nginx.conf </code></pre>

![Nginx](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/Nginx1.PNG) <br />

#### 5.6.1.	Instalando la aplicación.
Ahora se va a crear el directorio bookstore. Tenga presente que para poder realizar la copia por favor cambie los permisos en el directorio destino:
<pre><code> $ chmod 777 /usr/share/nginx/html/bookstore </code></pre>

Descargue y descomprima el código de la aplicación en su estación de trabajo (igual lo puede hacer en la máquina server) que se encuentra en EAFIT Interactiva. Va a observar que se crea la siguiente estructura de directorios:
![app1](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/app1.PNG) <br />

Proceda a  instalar node.js en la máquina de la siguiente forma:
<pre><code> $ sudo yum install -y gcc-c++ make 
 $ curl -sL https://rpm.nodesource.com/setup_14.x | sudo -E bash -
</code></pre>

Ahora si instalemos la versión de node.js:
<pre><code> $ sudo yum install -y nodejs </code></pre>

Verifiquemos la versión:
<pre><code> $ node -v
 $ npm -v 
</code></pre>

Ahora se requiere que instale las dependencias, para esto ubicado en el directorio front end ejecute el comando:
<pre><code> $ npm install 
</code></pre>

Va a observar que se crea la carpeta node_modules y queda la estructura de la siguiente forma:
![app2](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/app2.PNG) <br />

Para efectos de este laboratorio, nos interesa generar el código compilado de producción para la aplicación desarrollada. Para esto, realizaremos lo siguiente:
<pre><code> $ cd frontend
</code></pre>

Dado que la aplicación esta construida en React, se requiere crear los diferentes archivos para el entorno de producción. Para esto se requiere que ejecute el comando:
<pre><code> $ npm run build
</code></pre>

Posterior a la ejecución de este comando se creará la carpeta build, la cual contiene el código html, css, imágenes que se deben publicar en nuestro servidor web. 
![app2](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/app2.PNG) <br />

Copie la carpeta build desde su máquina (o desde el lugar donde la tiene) hasta el directorio bookstore que se creo en la instancia de EC2. En caso de que este en una máquina remota, procedamos a realizar una copia segura a través del siguiente comando:
<pre><code> $ scp -i xxx.pem -r /path/build/* ec2-user@ec2-X-X-X-X.compute-1.amazonaws.com:/usr/share/nginx/html/bookstore
</code></pre>

Nota: 
•	XXX.pem es el archivo que usted genero para conectarse a la máquina. 
•	/path equivale a la ruta donde usted tiene ubicado la carpeta backend del proyecto.
•	ec2-user@ec2X-X-X-X.compute-1.amazonaws.com
•	:/home/ec2-user : la ruta donde va a copiar los archivos en el servidor destino.

Cambie los permisos al directorio
<pre><code> $ chmod 777 /usr/share/nginx/html/bookstore/ </code></pre>

Ahora, se procede a verificar el estado del servicio web:
<pre><code> $ sudo systemctl status nginx.service </code></pre>

Si el servicio esta caído, por favor suba el servicio.
<pre><code> $ sudo systemctl start nginx.service </code></pre>

![app3](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/app3.PNG) <br />
<pre><code> $ sudo chkconfig nginx on </code></pre>


### 5.7.  Configuración de base de datos: MongoDB
Cree un archivo /etc/yum.repos.d/mongodb-org-5.0.repo para que pueda instalar MongoDB directamente usando yum:

<pre><code>[mongodb-org-5.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/amazon/2/mongodb-org/5.0/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-5.0.asc
</code></pre>

Para instalar la última versión estable de MongoDB, ejecute el siguiente comando:
<pre><code>$ sudo yum install -y mongodb-org</code></pre>

Puede iniciar el proceso mongod emitiendo el siguiente comando:
<pre><code> $ sudo systemctl start mongod</code></pre>

Puede verificar que el proceso de mongod se haya iniciado correctamente emitiendo el siguiente comando:
<pre><code> $ sudo systemctl status mongod</code></pre>

Inicie una sesión de mongosh en la misma máquina host que mongod. Puede ejecutar mongosh sin ninguna opción de línea de comandos para conectarse a un mongod que se está ejecutando en su localhost con el puerto predeterminado 27017.
<pre><code> $ mongosh</code></pre>

Ahora debe crear la base de datos con el siguiente comando:
<pre><code> > use bookstore </code></pre>

Y para crear la colección el siguiente:
<pre><code> > db.createCollection(books) </code></pre>

Y para insertar datos a la base de datos se usa el siguiente comando:
<pre><code> > db.books.insert({name: "...", author: "..."}) </code></pre>

La información que debe quedar en su base de datos debe ser esta:
![DATA1](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/DATA1.PNG) <br />
![DATA2](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/DATA2.PNG) <br />

Ahora vamos a configurar credenciales de nuestra base de datos para eso se sugieren los siguentes comandos:
<pre><code>
> use admin
</code></pre>

Luego se agrega el usuario que permitira crear otros usurios:
<pre><code>
> db.createUser(
  {
    user: "[user_name]",
    pwd: "[Password]",
    roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
  }
)
</code></pre>

Abra /etc/mongod.conf con su editor de código favorito y busque las siguientes líneas:
<pre><code>
security:
    authorization: "disabled"
</code></pre>

Cambie "disabled" por "enabled", guarde el archivo y reinicie mongod:
<pre><code>
 $ sudo service mongodb restart
</code></pre>

Ahora cree un usuario para la base de datos previamente creada de la mism aforma.

Por ultimo en el archivo .ENV ubicado en la carpeta del back end, agregue el siguente string de conexión a la base de datos.
mongodb+srv://<user>:<password>@<servers_elacstic_ip>:27017/myFirstDatabase?retryWrites=true&w=majority


### 5.8.	Desplegando el back end.
Antes que todo debemos instalar la versión de node. Para esto configuremos el repositorio.
<pre><code> $ sudo yum install -y gcc-c++ make 
 $ curl -sL https://rpm.nodesource.com/setup_14.x | sudo -E bash -
</code></pre>

Ahora si instalemos la versión de node.js:
<pre><code> $ sudo yum install -y nodejs
</code></pre>

Verifiquemos la versión:
<pre><code> $ node -v
 $ npm -v 
</code></pre>

Creemos un pequeño servidor web para verificar funcionalmente que todo este correcto, para esto cree un archivo en el directorio raíz de la aplicación:
<pre><code> $ sudo nano TestServer.js
</code></pre>

<pre><code>var http = require('http');
http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.end('Welcome Node.js');
}).listen(3000, "127.0.0.1");
console.log('Server running at http://127.0.0.1:3000/');
</code></pre>

Para ejecutar este código digite el comando: 
<pre><code> $ node TestServer.js
</code></pre>
![app4](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/app4.PNG) <br />

Se procede a realizar la copia de los archivos:
<pre><code> scp -i XXXX.pem -r /path/backend/ ec2-user@ec2X-X-X-X.compute-1.amazonaws.com:/home/ec2-user
</code></pre>

Nota: 
•	XXX.pem es el archivo que usted genero para conectarse a la máquina. 
•	/path equivale a la ruta donde usted tiene ubicado la carpeta backend del proyecto.
•	ec2-user@ec2X-X-X-X.compute-1.amazonaws.com
•	:/home/ec2-user : la ruta donde va a copiar los archivos en el servidor destino.

Ahora entramos al directorio backend y ejecutamos el comando;
<pre><code> $ npm install
</code></pre>

Esto permitirá la instalación de los módulos

En este punto debemos permitir el acceso a la bases de datos a nuestro servidor de bases de datos en la nube
<pre><code> $ node server.js
</code></pre>

Ahora configuramos el web server (nginx) para que reciba las peticiones dirigidas a la api: /api/books y las redirecciones al backend.
![flujo2](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/flujo2.PNG) <br />

Para esto agregamos la directiva upstream antes de la de server en el archivo nginx.conf
<pre><code> $ sudo nano /etc/nginx/nginx.conf
</code></pre>

<pre><code>upstream backend{
        server 172.31.50.214:5000;
    }
</code></pre>

Luego modificamos la directiva server y, dentro de esta, agregamos lo siguiente:
<pre><code>location /api/books {
        proxy_pass http://backend;
        }
</code></pre>

Al final, el archivo queda con el siguiente aspecto:
![app5](https://github.com/clopezr9/BookStore-Lab/blob/main/ImagenesBookStore/app5.PNG) <br />

### 5.9.	Verificación de la aplicación:
En un browser seleccione coloque la dirección IP elástica del front end y debe visualizar la página!
