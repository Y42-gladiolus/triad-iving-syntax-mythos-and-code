================================================================================
                    D - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Modern Systems Programming + C++ Compatibility
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка D (DMD/LDC/GDC)
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами (dub)
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые библиотеки

================================================================================
1. УСТАНОВКА D
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    D = MODERN SYSTEMS PROGRAMMING                            │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  D используется:                                                             │
│  • Systems programming                                                      │
│  • Game development                                                         │
│  • High-performance applications                                            │
│  • Compiler/interpreter development                                         │
│  • C++ migration                                                            │
│  • Embedded systems                                                         │
│                                                                              │
│  • 20+ лет развития (2001-2024)                                             │
│  • 3 компилятора (DMD, LDC, GDC)                                            │
│  • C++ совместимость                                                        │
│  • Garbage collection (можно отключить)                                     │
│  • Compile-time execution                                                   │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Вариант 1: Через официальный скрипт
curl -fsS https://dlang.org/install.sh | bash -s

# Вариант 2: Через apt
sudo apt update
sudo apt install dmd dub

# Вариант 3: LDC (LLVM-based, лучше оптимизации)
sudo apt install ldc

# Проверка
dmd --version
dub --version

macOS (Homebrew):
-----------------
brew install dmd
brew install dub

# Проверка
dmd --version

Windows:
--------
# Скачать с https://dlang.org/download.html
# Установщик .exe включает DMD и dub
# Добавить в PATH: C:\dmd2\windows\bin

# Проверка в PowerShell:
dmd --version

Docker (универсально):
----------------------
docker run -it --rm dlang2/dmd-ubuntu dmd --version

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для D                                               │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ Visual Studio   │ ★★★★★ - С D plugin (Windows)                              │
│ VS Code         │ ★★★★★ - С code-d extension (кроссплатформенный)           │
│ Dlang IDE       │ ★★★★★ - Официальная IDE (Windows)                         │
│ Vim/Neovim      │ ★★★★☆ - С vim-d                                            │
│ Emacs           │ ★★★★☆ - С d-mode                                           │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка VS Code + code-d:
---------------------------
1. Extensions (Ctrl+Shift+X)
2. Установить: "code-d" от WebFreak001
3. Установить: "D Language" от D Language Foundation
4. Автоматическая настройка

Установка Dlang IDE:
--------------------
# Скачать с https://wiki.dlang.org/DlangIDE
# Только Windows/Linux

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# D REPL (rdmd)
rdmd -e 'writeln("Hello, D!");'

# Создание проекта
dub init my_project
cd my_project

# Структура проекта:
my_project/
├── dub.json         # Конфигурация проекта
├── source/          # Исходный код
│   └── app.d        # Главный файл
└── .dub/            # Сборка

# Простая программа (source/app.d)
import std.stdio;

void main() {
    writeln("Hello, D!");
}

# Компиляция
dmd source/app.d

# Запуск
./app

# Через dub (рекомендуется)
dub run

# Компиляция с оптимизациями
dmd -O -release source/app.d

# BetterC mode (без GC)
dmd -betterC source/app.d

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ (DUB)
================================================================================

# Dub (D package manager)

# dub.json файл:
{
    "name": "my_project",
    "description": "My D project",
    "authors": ["John Doe"],
    "license": "MIT",
    "dependencies": {
        "vibe-d": "~>0.9.0",
        "mir": "~>4.0.0"
    }
}

# Популярные пакеты:
# - vibe-d (web framework)
# - mir (numerical computing)
# - dplug (audio plugins)
# - derelict (C bindings)

# Установка зависимостей
dub upgrade

# Поиск пакетов
# https://code.dlang.org/

# Создание библиотеки
dub init --type=library my_lib

# Публикация пакета
dub register
dub publish

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: Три компилятора
   DMD vs LDC vs GDC могут отличаться
   
   Решение:
   DMD для разработки (быстрая компиляция)
   LDC для production (лучшие оптимизации)

⚠️ Проблема 2: Garbage collection
   GC может вызывать паузы
   
   Решение:
   Использовать -betterC для отключения
   Или использовать @nogc функции

⚠️ Проблема 3: Windows совместимость
   Некоторые пакеты не работают на Windows
   
   Решение:
   Проверять cross-platform поддержку
   Использовать vibe-d для web

⚠️ Проблема 4: Меньше сообщество
   Меньше чем C++/Rust
   
   Решение:
   Присоединиться к D forum
   Читать D documentation

⚠️ Проблема 5: IDE поддержка
   Меньше чем mainstream языки
   
   Решение:
   Использовать VS Code + code-d
   Или Dlang IDE

⚠️ Проблема 6: C++ интероперабельность
   Может быть сложной
   
   Решение:
   Использовать derelict библиотеки
   Или писать C bindings вручную

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias d='dmd'" >> ~/.bashrc
echo "alias d='dmd'" >> ~/.zshrc

echo "alias drun='dub run'" >> ~/.bashrc
echo "alias drun='dub run'" >> ~/.zshrc

echo "alias dbuild='dub build'" >> ~/.bashrc
echo "alias dbuild='dub build'" >> ~/.zshrc

echo "alias dtest='dub test'" >> ~/.bashrc
echo "alias dtest='dub test'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия D
dmd --version

# Тест 2: Версия dub
dub --version

# Тест 3: Простая программа
echo 'import std.stdio; void main() { writeln("OK"); }' | dmd -run -

# Тест 4: Создание проекта
dub init test_project
cd test_project
dub run
cd ..
rm -rf test_project

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ БИБЛИОТЕКИ
================================================================================

# Базовые библиотеки (dub.json):

# Web framework
"dependencies": {
    "vibe-d": "~>0.9.0"
}

# Numerical computing
"dependencies": {
    "mir": "~>4.0.0"
}

# JSON parsing
"dependencies": {
    "vibe-d": "~>0.9.0"
}

# Database
"dependencies": {
    "mysql-native": "~>3.0.0"
}

# Testing
"dependencies": {
    "unit-threaded": "~>1.0.0"
}

# C bindings
"dependencies": {
    "derelict-util": "~>3.0.0"
}

================================================================================
                         КОНЕЦ README_D
================================================================================
