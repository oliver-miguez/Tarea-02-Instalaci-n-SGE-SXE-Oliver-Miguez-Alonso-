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
