================================================================================
                    COBOL - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Banking + Mainframe + 60+ лет эволюции
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка COBOL (GnuCOBOL)
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые библиотеки

================================================================================
1. УСТАНОВКА COBOL
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    COBOL = BANKING + MAINFRAME + LEGACY                      │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  COBOL используется:                                                         │
│  • Банковские системы                                                       │
│  • Мейнфреймы (IBM z/OS)                                                    │
│  • Legacy enterprise systems                                                │
│  • Government systems                                                       │
│  • Insurance и finance                                                      │
│                                                                              │
│  • Создан в 1959 году                                                       │
│  • 60+ лет развития                                                         │
│  • До сих пор работает в production                                         │
│  • GnuCOBOL (open source)                                                   │
│  • IBM Enterprise COBOL (commercial)                                        │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# GnuCOBOL (рекомендуется!)
sudo apt update
sudo apt install gnucobol4

# Или из исходников
wget https://sourceforge.net/projects/gnucobol/files/gnucobol/4.0/gnucobol-4.0.tar.gz
tar xzf gnucobol-4.0.tar.gz
cd gnucobol-4.0
./configure
make
sudo make install

# Проверка
cobc --version
cobol --version

macOS (Homebrew):
-----------------
brew install gnucobol

# Проверка
cobc --version

Windows:
--------
# TinyCOBOL или GnuCOBOL
# Скачать с https://sourceforge.net/projects/gnucobol/
# Установщик .exe

# Проверка в PowerShell:
cobc --version

Docker (универсально):
----------------------
docker run -it --rm openmainframeproject/cobol cobc --version

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для COBOL                                           │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ VS Code         │ ★★★★★ - С COBOL extension (от Broadcom)                   │
│ Eclipse         │ ★★★★★ - С IBM Enterprise COBOL plugin                     │
│ Vim/Neovim      │ ★★★★☆ - С cobol.vim                                       │
│ Emacs           │ ★★★★☆ - С cobol-mode                                        │
│ IntelliJ        │ ★★★☆☆ - С COBOL plugin                                    │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка VS Code + COBOL:
--------------------------
1. Extensions (Ctrl+Shift+X)
2. Установить: "COBOL" от Broadcom Ltd
3. Установить: "COBOL Language Support"

Установка Vim + cobol.vim:
--------------------------
# Через vim-plug:
Plug 'vim-scripts/cobol.vim'

Установка Emacs + cobol-mode:
-----------------------------
# Встроен в Emacs
(add-to-list 'auto-mode-alist '("\\.cob$" . cobol-mode))

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# COBOL компиляция
cobc -x program.cob

# Запуск
./program

# Compile and run
cobc -x -o program program.cob
./program

# COBOL программа (файл .cob или .cbl)
       IDENTIFICATION DIVISION.
       PROGRAM-ID. HELLO.
       PROCEDURE DIVISION.
           DISPLAY "Hello, COBOL!".
           STOP RUN.

# Создание проекта
mkdir my_project && cd my_project

# Структура проекта:
my_project/
├── src/             # Исходный код
│   └── program.cob
├── copybooks/       # Copybooks (include files)
├── data/            # Данные
└── Makefile         # Сборка

# Makefile пример:
CC=cobc
CFLAGS=-x -free
TARGET=program
SRC=program.cob

all: $(TARGET)

$(TARGET): $(SRC)
	$(CC) $(CFLAGS) -o $@ $<

clean:
	rm -f $(TARGET)

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ
================================================================================

# COBOL не имеет пакетного менеджера
# Copybooks = include files

# Copybooks (.cpy файлы)
# 01  CUSTOMER-RECORD.
#     05  CUSTOMER-ID    PIC 9(5).
#     05  CUSTOMER-NAME  PIC X(30).

# Использование copybook
       01  CUSTOMER-DATA.
           COPY CUSTOMER.CPY.

# GnuCOBOL библиотеки
# Встроены в GnuCOBOL:
# - libcob (runtime)
# - coblib (библиотеки)

# IBM COBOL libraries
# Требуют лицензию IBM

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: Разные диалекты COBOL
   GnuCOBOL vs IBM COBOL vs Micro Focus
   
   Решение:
   Использовать GnuCOBOL для обучения
   IBM COBOL для production мейнфреймов

⚠️ Проблема 2: Форматирование кода
   COBOL требует фиксированные колонки (традиционно)
   
   Решение:
   Использовать -free флаг для free format
   cobc -free program.cob

⚠️ Проблема 3: EBCDIC vs ASCII
   Мейнфреймы используют EBCDIC
   
   Решение:
   GnuCOBOL использует ASCII
   Для EBCDIC нужна конвертация

⚠️ Проблема 4: Copybooks не найдены
   COPY книга не находится
   
   Решение:
   Указать путь: cobc -I /path/to/copybooks
   Или установить COBCPY环境变量

⚠️ Проблема 5: Runtime ошибки
   Программа падает с cobol runtime error
   
   Решение:
   Проверить PIC clauses
   Проверить границы массивов

⚠️ Проблема 6: Компиляция не работает
   cobc: command not found
   
   Решение:
   export PATH=/usr/local/bin:$PATH
   Добавить в ~/.bashrc

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias cob='cobc'" >> ~/.bashrc
echo "alias cob='cobc'" >> ~/.zshrc

echo "alias cobx='cobc -x'" >> ~/.bashrc
echo "alias cobx='cobc -x'" >> ~/.zshrc

echo "alias cobf='cobc -free'" >> ~/.bashrc
echo "alias cobf='cobc -free'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия GnuCOBOL
cobc --version

# Тест 2: Простая программа
echo '       IDENTIFICATION DIVISION.
       PROGRAM-ID. TEST.
       PROCEDURE DIVISION.
           DISPLAY "OK".
           STOP RUN.' > test.cob
cobc -x test.cob
./test
rm test.cob test

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ БИБЛИОТЕКИ
================================================================================

# Базовые библиотеки:

# GnuCOBOL runtime
# Встроено в GnuCOBOL

# Copybooks библиотеки
# https://github.com/openmainframeproject/cobol-check

# IBM COBOL libraries
# Требуют лицензию IBM

# Micro Focus COBOL
# https://www.microfocus.com/products/visual-cobol/

# Утилиты:
# cobc (компилятор)
# cobcrun (runtime)
# cobconfig (конфигурация)

================================================================================
                         КОНЕЦ README_COBOL
================================================================================
