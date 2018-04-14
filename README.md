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

1). Baixe o script

```
wget https://raw.githubusercontent.com/summerblue/laravel-ubuntu-init/master/deploy-16.sh -O deploy.sh
chmod +x deploy.sh
```

sudo vim deploy.sh
e editar a senha:
# Configure
MYSQL_ROOT_PASSWORD="{{--Your Password--}}"
MYSQL_NORMAL_USER="estuser"
MYSQL_NORMAL_USER_PASSWORD="{{--Your Password--}}"
depois de instalar:
cd /data/www/{DIRETORIO DO SEU PROJETO}
chown www:www -R ./
permissão de root para o diretório
adicionar um site
 908 b
 Exemplo de arquivo config Nginx para Laravel
deve ser salvo no diretório /etc/nginx/sites-enabled
por exemplo: /etc/nginx/sites-enabled/exemplo.org
