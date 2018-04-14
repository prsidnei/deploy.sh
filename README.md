## Introdução

Shell script para setar um ambiente de produção do Laravel no Ubuntu.

## Vai instalar os seguintes programas:

* Git
* PHP 7.1
* Nginx
* MySQL
* Sqlite3
* Composer
* Node 6 (With Yarn, PM2, Bower, Grunt, and Gulp)
* Redis
* Memcached
* Beanstalkd

## Instalação

1) Baixe o script

```
wget https://raw.githubusercontent.com/prsidnei/setup-laravel-nginx/master/deploy.sh -O deploy.sh
chmod +x deploy.sh
```
2) Configure a senha do MySQL

`sudo vim deploy.sh` e edite a senha:

```
# Configure
MYSQL_ROOT_PASSWORD="{{--Your Password--}}"
MYSQL_NORMAL_USER="estuser"
MYSQL_NORMAL_USER_PASSWORD="{{--Your Password--}}"
```

3) Inicie a instalação

Execute o shell script:

```
sudo ./deploy.sh
```

A instalação será finalizada com esta mensagem:

```
"Esta Feito!!!!."
"Mysql Root Password: ${MYSQL_ROOT_PASSWORD}"
"Mysql Normal User: ${MYSQL_NORMAL_USER}"
"Mysql Normal User Password: ${MYSQL_NORMAL_USER_PASSWORD}"
```

## Após a instalação:

### 1. Permissão de root para o usuário Web

O Nginx usa o usuário `www`, e para que tudo funcione corretamente você deve alterar as permissões diretório:

```
cd /data/www/{DIRETORIO DO SEU PROJETO}
chown www:www -R ./
```
### 2. Adicionar um site

Template de arquivo de configuração do Nginx para Laravel que deverá ser salvo no diretório `/etc/nginx/sites-enabled`.
Por exemplo: `/etc/nginx/sites-enabled/exemplo.org`

```
server {
    listen 80;
    server_name {{---SEU DOMINIO---}};
    root "{{---DIRETORIO DO PROJETO---}}";

    index index.html index.htm index.php;

    charset utf-8;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }

    access_log /data/log/nginx/{{---NOME DO PROJETO---}}-access.log;
    error_log  /data/log/nginx/{{---NOME DO PROJETO---}}-error.log error;

    sendfile off;

    client_max_body_size 100m;

    include fastcgi.conf;

    location ~ /\.ht {
        deny all;
    }

    location ~ \.php$ {
        fastcgi_pass   127.0.0.1:9000;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
        include        fastcgi_params;
    }
}
```
Restartar o Nginx:

```
service nginx restart
```
