================================================================================
                    C++ - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Systems Programming + Performance + 40+ лет эволюции
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка C++ (GCC/Clang/MSVC)
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами (vcpkg/conan)
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые библиотеки

================================================================================
1. УСТАНОВКА C++
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    C++ = SYSTEMS PROGRAMMING + PERFORMANCE                   │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  C++ используется:                                                           │
│  • Systems programming                                                      │
│  • Game development                                                         │
│  • High-frequency trading                                                   │
│  • Embedded systems                                                         │
│  • Performance-critical applications                                        │
│                                                                              │
│  • 40+ лет развития (1983-2024)                                             │
│  • C++11/14/17/20/23 стандарты                                              │
│  • Zero-cost abstractions                                                   │
│  • Manual memory management                                                 │
│  • Template metaprogramming                                                 │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# GCC (GNU Compiler Collection)
sudo apt update
sudo apt install build-essential g++

# Clang (альтернатива)
sudo apt install clang

# Проверка
g++ --version
clang++ --version

# C++ стандарты
g++ -std=c++11 program.cpp  # C++11
g++ -std=c++14 program.cpp  # C++14
g++ -std=c++17 program.cpp  # C++17
g++ -std=c++20 program.cpp  # C++20

macOS (Homebrew):
-----------------
brew install gcc
# Или использовать Xcode command line tools
xcode-select --install

# Проверка
g++ --version

Windows:
--------
# MSVC (Microsoft Visual C++)
# Скачать Visual Studio Community с https://visualstudio.microsoft.com/
# Выбрать "Desktop development with C++"

# Или MinGW-w64
# Скачать с https://www.mingw-w64.org/

# Проверка в PowerShell:
g++ --version

Docker (универсально):
----------------------
docker run -it --rm gcc:latest g++ --version
docker run -it --rm ubuntu:latest g++ --version

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для C++                                             │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ Visual Studio   │ ★★★★★ - Лучшая для Windows (MSVC)                         │
│ CLion           │ ★★★★★ - Лучшая кроссплатформенная (JetBrains)             │
│ VS Code         │ ★★★★★ - С C++ extension (бесплатная)                      │
│ Qt Creator      │ ★★★★★ - Отличная для GUI приложений                       │
│ Vim/Neovim      │ ★★★★☆ - С YouCompleteMe                                    │
│ Emacs           │ ★★★★☆ - С CEDET                                              │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка VS Code + C++:
------------------------
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

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# Создание проекта
mkdir my_project && cd my_project

# Структура проекта:
my_project/
├── src/             # Исходный код
│   └── main.cpp
├── include/         # Заголовочные файлы
│   └── header.h
├── build/           # Сборка
├── CMakeLists.txt   # CMake конфигурация
└── Makefile         # Makefile (альтернатива)

# Простая программа (main.cpp)
#include <iostream>

int main() {
    std::cout << "Hello, C++!" << std::endl;
    return 0;
}

# Компиляция
g++ -std=c++17 -o program main.cpp

# Запуск
./program

# CMake (рекомендуется для больших проектов)
mkdir build && cd build
cmake ..
make
./program

# Запуск с аргументами
./program arg1 arg2

# Отладка
g++ -g -o program main.cpp
gdb ./program

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ (VCPKG/CONAN)
================================================================================

# vcpkg (Microsoft)
git clone https://github.com/Microsoft/vcpkg.git
cd vcpkg
./bootstrap-vcpkg.sh
./vcpkg install package_name

# Использование в CMake
set(CMAKE_TOOLCHAIN_FILE ${CMAKE_SOURCE_DIR}/vcpkg/scripts/buildsystems/vcpkg.cmake)

# Conan (кроссплатформенный)
pip install conan
conan install package_name

# Использование в CMake
include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()

# Популярные пакеты:
# boost, eigen, fmt, spdlog, catch2, gtest

# CMakeLists.txt пример:
cmake_minimum_required(VERSION 3.10)
project(MyProject)

find_package(Boost REQUIRED COMPONENTS system)
target_link_libraries(my_program Boost::system)

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: Разные компиляторы
   GCC vs Clang vs MSVC могут отличаться
   
   Решение:
   Использовать стандартный C++
   Избегать compiler-specific extensions

⚠️ Проблема 2: C++ стандарты
   C++11 vs C++14 vs C++17 vs C++20
   
   Решение:
   Указывать -std=c++17 явно
   Проверять поддержку компилятором

⚠️ Проблема 3: Linker ошибки
   Undefined reference errors
   
   Решение:
   Проверить порядок файлов при компиляции
   Использовать extern для declarations

⚠️ Проблема 4: Header guards
   Multiple definition errors
   
   Решение:
   Использовать #pragma once
   Или традиционные header guards

⚠️ Проблема 5: Memory leaks
   Manual memory management
   
   Решение:
   Использовать smart pointers (unique_ptr, shared_ptr)
   Использовать RAII pattern

⚠️ Проблема 6: ABI совместимость
   Разные компиляторы = разные ABI
   
   Решение:
   Использовать один компилятор для всего проекта
   Или использовать C ABI для библиотек

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias cpp='g++'" >> ~/.bashrc
echo "alias cpp='g++'" >> ~/.zshrc

echo "alias cpp11='g++ -std=c++11'" >> ~/.bashrc
echo "alias cpp11='g++ -std=c++11'" >> ~/.zshrc

echo "alias cpp17='g++ -std=c++17'" >> ~/.bashrc
echo "alias cpp17='g++ -std=c++17'" >> ~/.zshrc

echo "alias cpp20='g++ -std=c++20'" >> ~/.bashrc
echo "alias cpp20='g++ -std=c++20'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия компилятора
g++ --version

# Тест 2: Простая программа
echo '#include <iostream>
int main() { std::cout << "OK" << std::endl; return 0; }' | g++ -x c++ - -o test && ./test && rm test

# Тест 3: C++17 features
echo '#include <iostream>
int main() { auto [a, b] = std::make_pair(1, 2); std::cout << a << std::endl; return 0; }' | g++ -std=c++17 -x c++ - -o test && ./test && rm test

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ БИБЛИОТЕКИ
================================================================================

# Базовые библиотеки:

# Boost (огромная коллекция)
# https://www.boost.org/

# STL (стандартная библиотека)
# Встроена в компилятор

# Популярные:
# fmt (formatting)
# spdlog (logging)
# eigen (linear algebra)
# catch2 (testing)
# gtest (testing)
# nlohmann/json (JSON)
# openssl (crypto)

# Установка через vcpkg:
./vcpkg install fmt spdlog eigen3 catch2 nlohmann-json

================================================================================
                         КОНЕЦ README_CPP
================================================================================
