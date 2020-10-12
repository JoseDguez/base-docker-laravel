# base-docker-laravel
Plantilla base para un entorno de desarrollo con WSL2 (Windows) / Ubuntu 20.04 y Laravel.

## Contenedores
Los contenedores incluidos en el archivo ```docker-compose.yml``` son los básicos para trabajar con Laravel sin problemas.
* **web**: Este contenedor es nuestro webserver, utilizando ***nginx***.
* **database**: Este contenedos es nuestro servicio base de datos, utilizando ***mariadb*** en su última versión.
* **php**: Este contenedor maneja la instalación de ***php 7.4***.
* **composer**: Este contenedor maneja ***composer***, util para ejecutar comandos de composer directamente desde docker sin necesidad de instalar en nuestro equipo local.
* **npm**: Este contenedor maneja la instalación de ***nodejs*** en su última versión, util para ejecutar comandos como ```npm install, npm run dev``` directamente desde docker sin necesidad de instalar en nuestro equipo local.
* **artisan**: Este contenedor nos permite acceder a los comandos de ***artisan*** directamente desde composer.

## Cómo utilizar
Primero, asegurate que [Docker esté instalado](https://docs.docker.com/docker-for-windows/install/) en tu equipo y después clona este repositorio en la ubicación de tu preferencia.

Una vez clonado el repositorio, abre una consola en la ruta donde clonaste el repositorio y ejecuta ```docker-compose up -d --build web```. Este comando levantará los contenedores para nuestro sitio y expondrá los siguientes servicios con los puertos definidos:
* **nginx** :8080
* **mariadb** :3306
* **php** :9000

Como ya se mencionó en el listado de contenedores disponibles, se incluye Composer, NPM y Artisan como contenedores independientes para poder utilizarlos sin necesidad de tener instaladas estas dependencias en nuestro equipo local. A continuación se muestra un ejemplo de como ejecutar comandos con estos contenedores:
* **Composer**: ```docker-compose run --rm composer update```
* **NPM**: ```docker-compose run --rm npm install```
* **Artisan**: ```docker-compose run --rm artisan make:controller UsersController```

##### Instalar Laravel
Antes de hacer nada, elimina el archivo [README.md](src/README.md). Una vez eliminado el archivo podemos seguir una de estas opciones:
* Clonar un repositorio ya existente o copiar todos los archivos de nuestro proyecto dentro de la carpeta ```/src/```.
* En consola nos dirigimos a la carpeta ```/src/``` y ejecutamos el comando ```docker-compose run --rm composer create-project laravel/laravel .``` Ojo con el **.** al final de comando, esto se hace ya que ```/src/``` será nuestra raiz del proyecto.

Una vez instalado el proyecto necesitamos modificar el archivo **.env** de Laravel para incluir las credenciales de la base de datos. Los valores serán:
* DB_CONNECTION=mysql
* DB_HOST=database **(nombre del contenedor en docker)**
* DB_PORT=3306 **(puerto expuesto en docker)**
* DB_DATABASE=**valor colocado en docker**
* DB_USERNAME=**valor colocado en docker**
* DB_PASSWORD=**valor colocado en docker**

##### Archivos a personalizar
* **.env**: Este archivo ubicado en la raíz de este repositorio contiene los parametros para la conexión de base de datos y son las que utilizará Docker para crear y conecarse a la base de datos. **OJO: no confundir con el archivo .env de Laravel.**
* **default.conf y nginx.conf**: Estos archivos contienen la configuración del servidor ***nginx***, puedes modificar la configuración a tus necesidades. Puedes encontrar un ejemplo completo de la configuración [aquí](https://www.nginx.com/resources/wiki/start/topics/examples/full/).
* **www.conf**: Contiene una configuración para ***php-fpm*** utilizado en nuestro contenedor.
* **docker-compose.yml**: El archivo con la configuración para nuestra red de Docker, puedes modificarlo según tus necesidades.