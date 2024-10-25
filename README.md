как в битриксе быстро подключить composer

установка - https://getcomposer.org/download/
нужно перейти в папку битрикс, там появится файл composer.phar

php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === 'dac665fdc30fdd8ec78b38b9800061b4150413ff2e3b6f88543c636f7cd84f6db9189d43a81e5503cda447da73c7e5b6') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"

далее в папке битиркс исполняем команду
$ COMPOSER=composer-bx.json php composer.phar install
$ COMPOSER=composer-bx.json php composer.phar install require --dev symfony/var-dumper

Далее нам нужно подключить его (можно и без этого, но будет неудобно)
идем, например, в local/php_interface/init.php 

if (file_exists($_SERVER['DOCUMENT_ROOT'] . '/bitrix/vendor/autoload.php')) {
    require_once($_SERVER['DOCUMENT_ROOT'] . '/bitrix/vendor/autoload.php');
}
