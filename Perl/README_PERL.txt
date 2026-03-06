================================================================================
                    PERL - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Text Processing + Regex Master + 35+ лет эволюции
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка Perl (CPAN)
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами (CPAN)
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые модули

================================================================================
1. УСТАНОВКА PERL
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    PERL = LINGUIST CREATED + REGEX MASTER                    │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  Perl используется:                                                          │
│  • Text processing (лучше AWK)                                              │
│  • System administration                                                    │
│  • Web development (CGI)                                                    │
│  • Bioinformatics                                                           │
│  • Network programming                                                      │
│                                                                              │
│  • Создан лингвистом Larry Wall                                             │
│  • Мощные регулярные выражения                                              │
│  • 35+ лет развития (1987-2024)                                             │
│  • CPAN (огромная библиотека модулей)                                       │
│  • "There's More Than One Way To Do It"                                     │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Perl обычно предустановлен
perl --version

# Если нет:
sudo apt update
sudo apt install perl perl-doc

# CPAN (Comprehensive Perl Archive Network)
cpan

# Проверка
perl --version
cpan --version

macOS (Homebrew):
-----------------
# Perl предустановлен
perl --version

# Или новая версия:
brew install perl

Windows:
--------
# Strawberry Perl (рекомендуется!)
# Скачать с https://strawberryperl.com/
# Установщик .exe включает CPAN

# Проверка в PowerShell:
perl --version

Docker (универсально):
----------------------
docker run -it --rm perl:latest perl --version

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для Perl                                            │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ Vim/Neovim      │ ★★★★★ - С perl.vim (отличная поддержка)                   │
│ Emacs           │ ★★★★★ - С cperl-mode                                        │
│ VS Code         │ ★★★★☆ - С Perl extension                                  │
│ Padre           │ ★★★★☆ - Perl IDE (специализированная)                     │
│ Teko            │ ★★★☆☆ - Специализированный Perl editor                    │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка Vim + perl.vim:
-------------------------
# Через vim-plug:
Plug 'vim-scripts/perl.vim'

Установка Emacs + cperl-mode:
-----------------------------
# Встроен в Emacs
(add-to-list 'auto-mode-alist '("\\.pl$" . cperl-mode))

Установка Padre IDE:
--------------------
# Debian/Ubuntu:
sudo apt install padre

# CPAN:
cpan install Padre

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# Perl REPL (через perl)
perl -de 1

# В REPL:
DB<1> print "Hello\n"
DB<2> q  # Выход

# One-liner
perl -e 'print "Hello\n"'

# Из файла
perl script.pl

# Perl скрипт (файл .pl)
#!/usr/bin/perl
print "Hello, World!\n";

# Запуск скрипта
chmod +x script.pl
./script.pl

# Создание проекта
mkdir my_project && cd my_project

# Структура проекта:
my_project/
├── script.pl        # Главный скрипт
├── lib/             # Модули
│   └── MyModule.pm
├── t/               # Тесты
└── README.md        # Документация

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ (CPAN)
================================================================================

# CPAN (Comprehensive Perl Archive Network)
# 200K+ модулей!

# Первый запуск (конфигурация)
cpan

# Поиск модулей
cpan search Module::Name

# Установка модуля
cpan install Module::Name

# Установка через cpanm (рекомендуется!)
curl -L https://cpanmin.us | perl - --self-upgrade
cpanm Module::Name

# Обновление модулей
cpan upgrade Module::Name

# Локальная установка
cpanm --local-lib=~/perl5 Module::Name

# Проект зависимости
# cpanfile
requires 'DBI', '1.643';
requires 'JSON', '4.02';

# Установка из cpanfile
cpanm --installdeps .

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: System Perl vs Local Perl
   Не ломайте system perl!
   
   Решение:
   Используйте perenv или plenv
   Или устанавливайте в ~/perl5

⚠️ Проблема 2: CPAN зависимости
   Модули могут иметь много зависимостей
   
   Решение:
   Используйте cpanm (автоматически разрешает)
   cpanm --notest для ускорения

⚠️ Проблема 3: Perl версии
   Perl 5 vs Perl 6 (Raku) - разные языки!
   
   Решение:
   Perl 5 = классический Perl
   Raku = Perl 6 (отдельный язык)

⚠️ Проблема 4: Модули не находятся
   PERL5LIB не настроен
   
   Решение:
   export PERL5LIB=~/perl5/lib/perl5
   Или использовать local::lib

⚠️ Проблема 5: Компиляция XS модулей
   Требует C компилятор
   
   Решение:
   sudo apt install build-essential

⚠️ Проблема 6: Тесты модулей падают
   Тесты могут падать на вашей системе
   
   Решение:
   cpanm --notest Module::Name
   Или сообщить автору модуля

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias pl='perl'" >> ~/.bashrc
echo "alias pl='perl'" >> ~/.zshrc

echo "alias plc='cpanm'" >> ~/.bashrc
echo "alias plc='cpanm'" >> ~/.zshrc

echo "alias plr='perl -de 1'" >> ~/.bashrc
echo "alias plr='perl -de 1'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия Perl
perl --version

# Тест 2: Простой one-liner
perl -e 'print "Hello\n"'

# Тест 3: CPAN
cpan --version

# Тест 4: Модуль
perl -Mstrict -Mwarnings -e 'print "OK\n"'

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ МОДУЛИ
================================================================================

# Базовые модули (cpanm install):

# Text processing
cpanm Regexp::Common
cpanm Text::CSV
cpanm JSON

# Web
cpanm LWP::UserAgent
cpanm HTTP::Tiny
cpanm Mojolicious

# Database
cpanm DBI
cpanm DBD::mysql
cpanm DBD::Pg

# Testing
cpanm Test::More
cpanm Test::Exception

# Utilities
cpanm Path::Tiny
cpanm List::Util
cpanm File::Slurper

# Modern Perl
cpanm Moose
cpanm Moo
cpanm Types::Standard

================================================================================
                         КОНЕЦ README_PERL
================================================================================
