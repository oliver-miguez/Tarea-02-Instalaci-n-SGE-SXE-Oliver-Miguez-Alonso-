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
