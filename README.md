# luis
Lamp Stack
linea
.........
1.URL del repositorio de GitHub donde se ha alojado el documento técnico escrito en Markdown.
https://github.com/luiszg99/luis.git

2.Descripción de la instalacion de phpMyAdmin en Ubuntu Server 18.04.
- actualizar los paquetes con `sudo apt update`
- instalar phpmyadmin con `sudo apt-get install phpmyadmin`

3.Descripción de la instalacion de Adminer.
acceder al al siguiente directorio con `cd /var/www/html` , luego `cd adminer` (si no existe crear con `mkdir adminer`) y añadir los siguientes enlaces de instalacion `sudo wget https://github.com/vrana/adminer/realeases/download/v4.7.3/adminer-4.7.3.mysql.phpdow` y `sudo mv adminer-4.7.3-mysql.php index.php`

4.Instalación del analizador de logs GoAccess para Apache Server.
introduccir los siguientes comandos de instalación `echo "deb http://deb.goaccess.io/ $(lsb_release -cs) main" sudo tee -a /etc/apt/sources.list.d/goaccess.list` , `wget -O - https://deb.goaccess.io/gnugpg.key sudo apt-key add -` , `sudo apt-get update` y `sudo apt-get install goaccess`

5.Control de acceso a un directorio con .htaccess.
- crear el directorio stats con `mkdir /var/www/html/stats`
- Lanzar el proceso de goaccess en background para generar los informes en segundo plano con
`sudo goaccess /var/log/apache2/access.log -o /var/www/html/stats/index.html --log-format=COMBINED --real-time-html &`
- crear el archivo de contraseñas para el usuario que accederá al directorio stats con `sudo htpasswd -c /home/luis/.htpasswd luis`
- crear el archivo .htaccess en el directorio que queremos proteger con usuario y contraseña. con el comando `sudo nano /var/www/html/stats/.htaccess`
- escribir dentro del archivo .htaccess 
AuthType Basic
AuthName "Restricted Content"
AuthUserFile /home/usuario/.htpasswd
Require valid-user
- editar el archivo configuración de Apache con `sudo nano /etc/apache2/sites-enabled/000-default.conf`
- añadir la siguiente sección dentro <VirtualHost *:80> y </VirtualHost>
<Directory "/var/www/html/stats">
  Options Indexes FollowSymLinks
  AllowOverride All
  Require all granted
</Directory>
- reiniciar el servicio de Apache con `sudo /etc/init.d/apache2 restart`

6.instalar mysql server,ssh,apache,php y php-mysql
- actualizar los paquetes con `sudo apt-get update`
- instalar mysql server con `sudo apt install mysql-server`
- instalar ssh con `sudo apt install ssh`
- instalar apache con `sudo apt install apache2`
- instalar php con `sudo apt install php` y sus librerías con `sudo apt install libapache2-mod-php`
- instalar php-mysql con `sudo apt install php-mysql`