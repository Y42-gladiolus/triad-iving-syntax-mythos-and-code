================================================================================
                    PHP - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Web Development + CMS + Huge Ecosystem
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка PHP
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами (Composer)
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые библиотеки

================================================================================
1. УСТАНОВКА PHP
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    PHP = WEB DEVELOPMENT + CMS                               │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  PHP используется:                                                           │
│  • Web development (77% of all websites)                                    │
│  • CMS (WordPress, Drupal, Joomla)                                          │
│  • E-commerce (Magento, WooCommerce)                                        │
│  • REST APIs                                                                │
│  • CLI scripting                                                            │
│                                                                              │
│  • 1995+ разработка                                                         │
│  • Написан на C (Zend Engine)                                               │
│  • Dynamic typing (с static в PHP 7+)                                       │
│  • Garbage collected                                                        │
│  • Web-first language                                                       │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Вариант 1: Через apt
sudo apt update
sudo apt install php php-cli php-mbstring php-xml php-curl

# Вариант 2: Через Ondrej PPA (более новые версии)
sudo add-apt-repository ppa:ondrej/php
sudo apt update
sudo apt install php8.2 php8.2-cli php8.2-mbstring

# Проверка
php --version

macOS (Homebrew):
-----------------
brew install php

# Проверка
php --version

Windows:
--------
# Скачать с https://windows.php.net/download/
# Распаковать архив
# Добавить в PATH

# Проверка в PowerShell:
php --version

Docker (универсально):
----------------------
docker run -it --rm php:latest php --version

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для PHP                                             │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ PhpStorm        │ ★★★★★ - Лучшая IDE для PHP (JetBrains)                    │
│ VS Code         │ ★★★★★ - С PHP extension (бесплатная)                      │
│ Vim/Neovim      │ ★★★★☆ - С php.vim                                          │
│ Emacs           │ ★★★★☆ - С php-mode                                           │
│ Sublime Text    │ ★★★★☆ - С PHP package                                       │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка VS Code + PHP:
------------------------
1. Extensions (Ctrl+Shift+X)
2. Установить: "PHP" от DEVSENSE
3. Установить: "PHP Intelephense" для IntelliSense
4. Установить: "PHP CS Fixer" для formatting

Установка PhpStorm:
-------------------
# Скачать с https://www.jetbrains.com/phpstorm/
# Платная IDE (бесплатная для студентов)

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# PHP REPL (psysh)
composer global require psy/psysh
psysh

# В psysh:
>>> 2 + 2
=> 4
>>> exit  # Выход

# Создание проекта
mkdir my_project && cd my_project

# Структура проекта:
my_project/
├── index.php      # Главный файл
├── composer.json  # Зависимости
└── README.md      # Документация

# Простая программа (index.php)
<?php
echo "Hello, PHP!";

# Запуск
php index.php

# Built-in web server
php -S localhost:8000

# Composer init
composer init

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ (COMPOSER)
================================================================================

# Composer (PHP package manager)

# Установка composer
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer

# composer.json файл:
{
    "name": "my/project",
    "description": "My project",
    "require": {
        "php": "^8.2",
        "laravel/framework": "^10.0"
    },
    "require-dev": {
        "phpunit/phpunit": "^10.0"
    },
    "autoload": {
        "psr-4": {
            "App\\": "src/"
        }
    }
}

# Установка зависимостей
composer install

# Обновление зависимостей
composer update

# Поиск пакетов:
# https://packagist.org/

# Популярные пакеты:
# - laravel/framework (web framework)
# - symfony/framework (enterprise framework)
# - phpunit/phpunit (testing)
# - monolog/monolog (logging)
# - guzzlehttp/guzzle (HTTP client)

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: Несколько версий PHP
   Разные проекты требуют разные версии
   
   Решение:
   Используйте phpenv или update-alternatives
   phpenv use 8.2

⚠️ Проблема 2: Missing extensions
   Некоторые библиотеки требуют расширения
   
   Решение:
   sudo apt install php-mbstring php-xml php-curl

⚠️ Проблема 3: Composer permissions
   Permission denied ошибки
   
   Решение:
   Не используйте sudo composer
   Используйте composer в home directory

⚠️ Проблема 4: memory_limit
   PHP memory limit слишком низкий
   
   Решение:
   Изменить в php.ini: memory_limit = 512M

⚠️ Проблема 5: Timezone warnings
   PHP warning про timezone
   
   Решение:
   date.timezone = "UTC" в php.ini

⚠️ Проблема 6: Deprecated функции
   Устаревшие функции в старом коде
   
   Решение:
   Обновить код до PHP 8+
   Использовать modern alternatives

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias php='php'" >> ~/.bashrc
echo "alias php='php'" >> ~/.zshrc

echo "alias composer='composer'" >> ~/.bashrc
echo "alias composer='composer'" >> ~/.zshrc

echo "alias phpserver='php -S localhost:8000'" >> ~/.bashrc
echo "alias phpserver='php -S localhost:8000'" >> ~/.zshrc

echo "alias composeri='composer install'" >> ~/.bashrc
echo "alias composeri='composer install'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия PHP
php --version

# Тест 2: Простое вычисление
echo "<?php echo 2 + 2;" | php

# Тест 3: Composer
composer --version

# Тест 4: Built-in server
php -S localhost:8000 &
curl http://localhost:8000
kill %1

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ БИБЛИОТЕКИ
================================================================================

# Базовые пакеты (composer.json):

# Web frameworks
"laravel/framework": "^10.0"
"symfony/framework-bundle": "^6.0"

# Database
"doctrine/orm": "^2.14"
"illuminate/database": "^10.0"

# Testing
"phpunit/phpunit": "^10.0"
"phpspec/phpspec": "^7.0"

# HTTP client
"guzzlehttp/guzzle": "^7.0"

# Logging
"monolog/monolog": "^3.0"

# Utilities
"vlucas/phpdotenv": "^5.0"
"symfony/var-dumper": "^6.0"

================================================================================
                         КОНЕЦ README_PHP
================================================================================
