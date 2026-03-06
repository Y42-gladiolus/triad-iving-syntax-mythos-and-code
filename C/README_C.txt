================================================================================
                    C - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Systems Programming + Foundation + 50+ лет эволюции
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка C (GCC/Clang)
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые библиотеки

================================================================================
1. УСТАНОВКА C
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    C = FATHER OF SYSTEMS PROGRAMMING                         │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  C используется:                                                             │
│  • Operating systems (Linux, Windows, macOS)                                │
│  • Embedded systems                                                         │
│  • Compilers и interpreters                                                 │
│  • Databases                                                                │
│  • Network protocols                                                        │
│                                                                              │
│  • 50+ лет развития (1972-2024)                                             │
│  • C89/C99/C11/C17/C23 стандарты                                            │
│  • Manual memory management                                                 │
│  • Direct hardware access                                                   │
│  • Foundation для C++, Objective-C, и др.                                   │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# GCC (GNU Compiler Collection)
sudo apt update
sudo apt install build-essential

# Clang (альтернатива)
sudo apt install clang

# Проверка
gcc --version
clang --version

# C стандарты
gcc -std=c89 program.c  # C89/C90
gcc -std=c99 program.c  # C99
gcc -std=c11 program.c  # C11
gcc -std=c17 program.c  # C17
gcc -std=c23 program.c  # C23

macOS (Homebrew):
-----------------
# Xcode command line tools
xcode-select --install

# Или GCC через Homebrew
brew install gcc

# Проверка
gcc --version

Windows:
--------
# MinGW-w64
# Скачать с https://www.mingw-w64.org/

# Или MSVC (Microsoft Visual C++)
# Скачать Visual Studio Community с https://visualstudio.microsoft.com/

# Проверка в PowerShell:
gcc --version

Docker (универсально):
----------------------
docker run -it --rm gcc:latest gcc --version
docker run -it --rm ubuntu:latest gcc --version

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для C                                               │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ Visual Studio   │ ★★★★★ - Лучшая для Windows (MSVC)                         │
│ CLion           │ ★★★★★ - Лучшая кроссплатформенная (JetBrains)             │
│ VS Code         │ ★★★★★ - С C/C++ extension (бесплатная)                    │
│ Vim/Neovim      │ ★★★★☆ - С YouCompleteMe                                    │
│ Emacs           │ ★★★★☆ - С CEDET                                              │
│ Eclipse         │ ★★★★☆ - С CDT plugin                                         │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка VS Code + C/C++:
--------------------------
1. Extensions (Ctrl+Shift+X)
2. Установить: "C/C++" от Microsoft
3. Установить: "C/C++ Extension Pack"
4. Установить: "CMake Tools"

Установка CLion:
----------------
# Скачать с https://www.jetbrains.com/clion/
# Платная (бесплатная для студентов)

Установка Visual Studio:
------------------------
# Скачать с https://visualstudio.microsoft.com/
# Community edition бесплатная
# Выбрать "Desktop development with C++"

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# Создание проекта
mkdir my_project && cd my_project

# Структура проекта:
my_project/
├── src/             # Исходный код
│   └── main.c
├── include/         # Заголовочные файлы
│   └── header.h
├── build/           # Сборка
└── Makefile         # Makefile

# Простая программа (main.c)
#include <stdio.h>

int main() {
    printf("Hello, C!\n");
    return 0;
}

# Компиляция
gcc -o program main.c

# Запуск
./program

# Компиляция с оптимизациями
gcc -O2 -o program main.c

# Компиляция с отладкой
gcc -g -o program main.c

# Makefile пример:
CC = gcc
CFLAGS = -Wall -Wextra -O2
TARGET = program
SRC = main.c

all: $(TARGET)

$(TARGET): $(SRC)
	$(CC) $(CFLAGS) -o $@ $<

clean:
	rm -f $(TARGET)

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ
================================================================================

# C не имеет пакетного менеджера
# Библиотеки = .a (static) или .so (shared)

# Популярные библиотеки:
# - libc (стандартная библиотека C)
# - libm (математическая библиотека)
# - libpthread (потоки)
# - libcurl (HTTP client)
# - libjson-c (JSON parsing)

# Установка через apt (Ubuntu/Debian)
sudo apt install libcurl4-openssl-dev
sudo apt install libjson-c-dev

# Компиляция с библиотеками
gcc -o program main.c -lcurl -ljson-c

# pkg-config (для нахождения библиотек)
gcc -o program main.c $(pkg-config --cflags --libs curl)

# CMake (для больших проектов)
cmake_minimum_required(VERSION 3.10)
project(MyProject)

find_package(CURL REQUIRED)
target_link_libraries(my_program CURL::libcurl)

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: Разные компиляторы
   GCC vs Clang vs MSVC могут отличаться
   
   Решение:
   Использовать стандартный C
   Избегать compiler-specific extensions

⚠️ Проблема 2: C стандарты
   C89 vs C99 vs C11 vs C17 vs C23
   
   Решение:
   Указывать -std=c11 явно
   Проверять поддержку компилятором

⚠️ Проблема 3: Memory leaks
   Manual memory management
   
   Решение:
   Всегда free() после malloc()
   Использовать valgrind для проверки

⚠️ Проблема 4: Buffer overflow
   Нет bounds checking
   
   Решение:
   Использовать snprintf вместо sprintf
   Проверять границы массивов

⚠️ Проблема 5: Pointer errors
   Dangling pointers, null pointers
   
   Решение:
   Инициализировать pointers в NULL
   Проверять перед использованием

⚠️ Проблема 6: Endianness
   Разный byte order на разных архитектурах
   
   Решение:
   Использовать htonll/ntohll для network byte order

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias c='gcc'" >> ~/.bashrc
echo "alias c='gcc'" >> ~/.zshrc

echo "alias c99='gcc -std=c99'" >> ~/.bashrc
echo "alias c99='gcc -std=c99'" >> ~/.zshrc

echo "alias c11='gcc -std=c11'" >> ~/.bashrc
echo "alias c11='gcc -std=c11'" >> ~/.zshrc

echo "alias c17='gcc -std=c17'" >> ~/.bashrc
echo "alias c17='gcc -std=c17'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия компилятора
gcc --version

# Тест 2: Простая программа
echo '#include <stdio.h>
int main() { printf("OK\n"); return 0; }' | gcc -x c - -o test && ./test && rm test

# Тест 3: C11 features
echo '#include <stdio.h>
#include <stdalign.h>
int main() { printf("OK\n"); return 0; }' | gcc -std=c11 -x c - -o test && ./test && rm test

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ БИБЛИОТЕКИ
================================================================================

# Базовые библиотеки:

# Стандартная библиотека C
# - stdio.h (I/O)
# - stdlib.h (memory, utilities)
# - string.h (string operations)
# - math.h (mathematics)
# - pthread.h (threads)

# Популярные сторонние:
# - libcurl (HTTP client)
# - libjson-c (JSON parsing)
# - OpenSSL (crypto)
# - libsqlite3 (database)
# - libuv (async I/O)

# Установка через apt:
sudo apt install libcurl4-openssl-dev
sudo apt install libjson-c-dev
sudo apt install libssl-dev
sudo apt install libsqlite3-dev
sudo apt install libuv1-dev

================================================================================
                         КОНЕЦ README_C
================================================================================
