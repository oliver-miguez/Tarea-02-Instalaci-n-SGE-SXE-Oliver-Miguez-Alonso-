# Tarea 02 Instalacion WordPress - Server

## 1º Instalar Dependencias:
### Primero deberemos instalar las siguientes dependencias para poder instalar y ejetura todo de manera correcta: 

    sudo apt update

    sudo apt install apache2 \

                 ghostscript \
                 
                 libapache2-mod-php \
                 
                 mysql-server \
                 
                 php \
                 
                 php-bcmath \
                 
                 php-curl \
                 
                 php-imagick \
                 
                 php-intl \
                 
                 php-json \
                 
                 php-mbstring \
                 
                 php-mysql \
                 
                 php-xml \
                 
                 php-zip
                 

![Foto 1](https://github.com/oliver-miguez/Tarea-02-Instalacion-WordPress-Server-SXE-Oliver-Miguez-Alonso-/blob/main/1.png)

__________________________________________________________________________________________________________________________

## 2º Instalar WordPress
### Deberemos crear un directorio para la instalación y a continuación y descargar los archivos de Wordpress.org

    sudo mkdir -p /srv/www
    sudo chown www-data: /srv/www
    curl https://wordpress.org/latest.tar.gz | sudo -u www-data tar zx -C /srv/www
    
![Foto2](https://github.com/oliver-miguez/Tarea-02-Instalacion-WordPress-Server-SXE-Oliver-Miguez-Alonso-/blob/main/2.png)

__________________________________________________________________________________________________________________________

## 3º Configurar Apache para WordPress
### Debemos de crear un sitio Apache para WordPress

    <VirtualHost *:80>
        DocumentRoot /srv/www/wordpress
        <Directory /srv/www/wordpress>
            Options FollowSymLinks
            AllowOverride Limit Options FileInfo
            DirectoryIndex index.php
            Require all granted
        </Directory>
        <Directory /srv/www/wordpress/wp-content>
            Options FollowSymLinks
            Require all granted
        </Directory>
    </VirtualHost>
Y Activarla con los siguiente comandos por consola:
    
    sudo a2ensite wordpress
    
    sudo a2enmod rewrite
    
    sudo a2dissite 000-default
![Foto 3](https://github.com/oliver-miguez/Tarea-02-Instalacion-WordPress-Server-SXE-Oliver-Miguez-Alonso-/blob/main/3.png)

Y recargamos apache para que los cambios se guarden y funcionen correctamente :

    sudo service apache2 reload

__________________________________________________________________________________________________________________________


## 4º Configurar la base de datos
### Para configurar WordePress deberemos crear una base de datos , en este caso utilizaré MySql

![Foto 6](https://github.com/oliver-miguez/Tarea-02-Instalacion-WordPress-Server-SXE-Oliver-Miguez-Alonso-/blob/main/6.png)

Y la creamos , le damos permisos y salimos:

    mysql> CREATE DATABASE wordpress;
    Query OK, 1 row affected (0,00 sec)
    
    mysql> CREATE USER wordpress@localhost IDENTIFIED BY '<your-password>';
    Query OK, 1 row affected (0,00 sec)
    
    mysql> GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
        -> ON wordpress.*
        -> TO wordpress@localhost;
    Query OK, 1 row affected (0,00 sec)
    
    mysql> FLUSH PRIVILEGES;
    Query OK, 1 row affected (0,00 sec)
    
    mysql> quit
    Bye

## 5º Conectar WordPress a la base de datos
### Para comenzar debemos añadir esta linea a la consola:

    sudo -u www-data cp /srv/www/wordpress/wp-config-sample.php /srv/www/wordpress/wp-config.php
    
Y añadimos las siguientes credenciales : 

    sudo -u www-data sed -i 's/database_name_here/wordpress/' /srv/www/wordpress/wp-config.php
    sudo -u www-data sed -i 's/username_here/wordpress/' /srv/www/wordpress/wp-config.php
    sudo -u www-data sed -i 's/password_here/<your-password>/' /srv/www/wordpress/wp-config.php
    
![Imagen8](https://github.com/oliver-miguez/Tarea-02-Instalacion-WordPress-Server-SXE-Oliver-Miguez-Alonso-/blob/main/8.png)

Por último modificamos la configuracion :

    sudo -u www-data nano /srv/www/wordpress/wp-config.php

Encuentra esto:
    
    define( 'AUTH_KEY',         'put your unique phrase here' );
    define( 'SECURE_AUTH_KEY',  'put your unique phrase here' );
    define( 'LOGGED_IN_KEY',    'put your unique phrase here' );
    define( 'NONCE_KEY',        'put your unique phrase here' );
    define( 'AUTH_SALT',        'put your unique phrase here' );
    define( 'SECURE_AUTH_SALT', 'put your unique phrase here' );
    define( 'LOGGED_IN_SALT',   'put your unique phrase here' );
    define( 'NONCE_SALT',       'put your unique phrase here' );
    
![Foto9](https://github.com/oliver-miguez/Tarea-02-Instalacion-WordPress-Server-SXE-Oliver-Miguez-Alonso-/blob/main/9.png)

Borralo(ctrl+k). Luego remplaza el contenido con los valores que obtengas aqui: https://api.wordpress.org/secret-key/1.1/salt/. 

Guardalo y cierralo con Ctr+x

## Configurar WordPress
### Por último en tu navedor introduce lo siguiente:
    http://tuIpDelServer/

Configura , añadiendo nombre, contraseña, descargas y listo
