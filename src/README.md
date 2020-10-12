# Instalar Laravel
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