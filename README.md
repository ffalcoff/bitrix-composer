# Быстрое подключение Composer в Битрикс

## Установка Composer

Чтобы подключить Composer в Битрикс, следуйте шагам ниже:

1. Перейдите на сайт [getcomposer.org/download](https://getcomposer.org/download/) и выполните установку Composer.
   
2. Далее, в папке проекта `bitrix`, выполните следующие команды для установки Composer локально:

    ```bash
    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
    php -r "if (hash_file('sha384', 'composer-setup.php') === 'dac665fdc30fdd8ec78b38b9800061b4150413ff2e3b6f88543c636f7cd84f6db9189d43a81e5503cda447da73c7e5b6') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
    php composer-setup.php
    php -r "unlink('composer-setup.php');"
    ```

   После выполнения этих команд в директории появится файл `composer.phar`.

## Установка зависимостей

1. Убедитесь, что вы находитесь в папке `bitrix`, затем выполните команду для установки зависимостей из файла `composer-bx.json`:

    ```bash
    COMPOSER=composer-bx.json php composer.phar install
    ```

2. Для установки дополнительных пакетов, например `symfony/var-dumper`, выполните следующую команду:

    ```bash
    COMPOSER=composer-bx.json php composer.phar require --dev symfony/var-dumper
    ```

## Подключение автозагрузчика Composer

После установки, чтобы автоматически подключать зависимости, добавьте следующий код в файл `local/php_interface/init.php`:

```php
if (file_exists($_SERVER['DOCUMENT_ROOT'] . '/bitrix/vendor/autoload.php')) {
    require_once($_SERVER['DOCUMENT_ROOT'] . '/bitrix/vendor/autoload.php');
}
