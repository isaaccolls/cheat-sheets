- [install](#install)
- [built-in web server](#built-in-web-server)
- [code standard guide](#code-standard-guide)
- [composer](#composer)
- [testing](#testing)
- [docker](#docker)
- [xampp](#xampp)

# install

```bash
sudo add-apt-repository ppa:ondrej/php
sudo apt update
sudo apt-get install php8.1 php8.1-cli php8.1-common php8.1-fpm
```

- manage: `sudo systemctl status php8.1-fpm.service`

# built-in web server

`php -S localhost:8000 -t public`

# code standard guide

- [psr](https://www.php-fig.org/psr/)

## PHP_CodeSniffer

- run phpcs manually from shell `phpcs -sw --standard=PSR1 file.php`
- fix the code layout problems reported by PHP_CodeSniffer `phpcbf -w --standard=PSR1 file.php`
- show which kind of errors the code structure had before it fixed them `php-cs-fixer fix -v --rules=@PSR1 file.php`
- Command Line Interface `php -i` (_-i option_ will print PHP configuration) (_-a option_ provides an interactive shell)

# composer

## install

- [from official](https://getcomposer.org/download/) installs a _composer.phar_ binary in your current working directory
- install Composer globally: `mv composer.phar /usr/local/bin/composer`

## use

- composer require: `composer require twig/twig:^2.0`
- create a full composer.json: `composer init`
- download and install your dependencies into the _vendor/_ directory: `composer install`
- global dependencies: `composer global require phpunit/phpunit`
- after manaul update: `composer update --ignore-platform-reqs` 😉
- [official repository for Composer](https://packagist.org/)
- [PHP design patterns](https://designpatternsphp.readthedocs.io/en/latest/README.html)
- recompile loads of files creating the huge _bootstrap/compiled.php_: `composer dumpautoload -o`

## tell PHP to use Composer's autoloader

```php
<?php
require 'vendor/autoload.php';
```

# testing

[phpunit](https://phpunit.de/)

# docker

- Running PHP Applications in Docker: `docker run -d --name my-php-webserver -p 8080:80 -v /path/to/your/php/files:/var/www/html/ php:apache`
- [auto-generate](https://phpdocker.io/generator)

# xampp

## install xampp

1. download from <https://www.apachefriends.org/download.html>
2. set the permissions `sudo chmod +x xampp-linux-x64-7.2.0-0-installer.run`
3. install `sudo ./xampp-linux-x64-7.2.0-0-installer.run`
4. xampp will be installed on `/opt/lampp`
5. symbolic link for php `sudo ln -s /opt/lampp/bin/php /usr/local/bin/php`
6. symbolic link for mysql `sudo ln -s /opt/lampp/bin/mysql /usr/local/bin/mysql`
7. set a new ownership for htdocs `sudo chown -R [Username]:[Groupname] /opt/lampp/htdocs`
8. uninstall

```bash
cd /opt/lampp
sudo ./uninstall
# also should delete symbolic links 🤔
```

## use xampp

- xampp start `sudo /opt/lampp/lampp start`
- xampp stop `sudo /opt/lampp/lampp stop`
- xampp status `sudo /opt/lampp/lampp status`
- start manager `sudo -i /opt/lampp/manager-linux-x64.run`

## logs

- location `/var/log/apache2/error.log`
- send some error message

  ```php
  $databaseErrors = $stmt -> errorInfo();
  $errorInfo = print_r($databaseErrors, true);
  $errorLogMsg = "error info: $errorInfo";
  error_log($errorLogMsg);
  error_log("otra linea de error", 0);
  error_log(print_r($address), 0);
  ```
