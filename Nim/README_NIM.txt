================================================================================
                    NIM - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Python-синтаксис + Lisp-макросы + C-производительность
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка Nim (choosenim)
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами (Nimble)
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые пакеты

================================================================================
1. УСТАНОВКА NIM (CHOOSENIM)
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    NIM = PYTHON СИНТАКСИС + LISP МАКРОСЫ                     │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  Nim компилируется в:                                                        │
│  • C/C++ — для native производительности                                    │
│  • JavaScript — для web                                                     │
│  • Objective-C — для iOS/macOS                                              │
│                                                                              │
│  • Макросы (как Lisp)                                                       │
│  • Metaprogramming (DSL)                                                    │
│  • No GC (опционально)                                                      │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Вариант 1: Через choosenim (рекомендуется!)
curl https://nim-lang.org/choosenim/init.sh -sSf | sh

# Добавить в PATH
export PATH="$HOME/.nimble/bin:$PATH"
echo 'export PATH="$HOME/.nimble/bin:$PATH"' >> ~/.bashrc

# Вариант 2: Через apt (может быть старая версия)
sudo apt update
sudo apt install nim nimble

# Проверка
nim --version
nimble --version

macOS (Homebrew):
-----------------
brew install nim nimble

# Проверка
nim --version

Windows:
--------
# Скачать с https://nim-lang.org/install.html
# Установщик .exe включает choosenim
# Добавить в PATH: C:\Users\%USER%\nimble\bin

# Проверка в PowerShell:
nim --version

Docker (универсально):
----------------------
docker run -it --rm nimlang/nim nim --version

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для Nim                                             │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ VS Code         │ ★★★★★ - С Nim extension (официальный)                     │
│ Vim/Neovim      │ ★★★★☆ - С nim.vim + nimsuggest                            │
│ Emacs           │ ★★★★☆ - С nim-mode                                          │
│ IntelliJ IDEA   │ ★★★☆☆ - С Nim plugin                                      │
│ Sublime Text    │ ★★★☆☆ - С Nim package                                     │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка VS Code + Nim:
------------------------
1. Extensions (Ctrl+Shift+X)
2. Установить: "Nim" от Koshei
3. Установить: "Nimble" для управления пакетами

Установка nimsuggest (автодополнение):
--------------------------------------
nimble install nimsuggest

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# Создание проекта
nimble init my_project
cd my_project

# Структура проекта:
my_project/
├── my_project.nimble  # Конфигурация проекта
├── src/               # Исходный код
│   └── my_project.nim
└── tests/             # Тесты

# Запуск проекта
nimble run

# Компиляция
nim c -r src/my_project.nim

# Компиляция в release mode
nim c -d:release -r src/my_project.nim

# Форматирование
nimpretty src/my_project.nim

# Тесты
nimble test

# Документация
nim doc src/my_project.nim

# JavaScript target
nim js -r src/my_project.nim

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ (NIMBLE)
================================================================================

# Nimble = пакетный менеджер Nim

# Поиск пакетов
nimble search package_name

# Установка пакета
nimble install package_name

# Установка в проект
nimble install package_name --depsOnly

# Обновление пакетов
nimble update

# Удаление пакета
nimble uninstall package_name

# Список установленных
nimble list

# my_project.nimble файл:
# Package
version       = "0.1.0"
author        = "Your Name"
description   = "My project"
license       = "MIT"
srcDir        = "src"
bin           = @["my_project"]

# Зависимости
requires "nim >= 1.6.0"
requires "chronos >= 4.0.0"

# Опубликовать пакет
nimble publish

# Сообщество пакеты:
# https://nimble.directory/

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: nimble не в PATH
   nimble: command not found
   
   Решение:
   export PATH="$HOME/.nimble/bin:$PATH"
   Добавить в ~/.bashrc

⚠️ Проблема 2: Конфликт версий
   Разные проекты требуют разные версии
   
   Решение: choosenim manage версии
   choosenim 1.6.0
   choosenim stable

⚠️ Проблема 3: C компилятор не найден
   Nim требует GCC/Clang для компиляции
   
   Решение:
   sudo apt install build-essential

⚠️ Проблема 4: Пакеты не находятся
   Cannot find module
   
   Решение:
   nimble install --depsOnly

⚠️ Проблема 5: nimsuggest не работает
   Автодополнение не работает
   
   Решение:
   nimble install nimsuggest
   Перезапустить VS Code

⚠️ Проблема 6: GC проблемы
   Garbage collector вызывает паузы
   
   Решение:
   Compile with -d:gc:arc или -d:gc:orc
   Или --gc:manual для полного контроля

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias n='nim'" >> ~/.bashrc
echo "alias n='nim'" >> ~/.zshrc

echo "alias nb='nimble'" >> ~/.bashrc
echo "alias nb='nimble'" >> ~/.zshrc

echo "alias nr='nim c -r'" >> ~/.bashrc
echo "alias nr='nim c -r'" >> ~/.zshrc

echo "alias nf='nimpretty'" >> ~/.bashrc
echo "alias nf='nimpretty'" >> ~/.zshrc

echo "alias nt='nimble test'" >> ~/.bashrc
echo "alias nt='nimble test'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия Nim
nim --version

# Тест 2: Версия Nimble
nimble --version

# Тест 3: Простое вычисление
echo 'echo 2 + 2' | nim c -r -

# Тест 4: Создание и запуск проекта
nimble init test_project
cd test_project
nimble run
cd ..
rm -rf test_project

# Тест 5: Компиляция в JS
echo 'echo "Hello"' | nim js -

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ ПАКЕТЫ
================================================================================

# Базовые пакеты (nimble install):

# HTTP клиент
nimble install httpbeast
nimble install requests

# JSON парсинг
# Встроено в stdlib (json)

# Асинхронность
nimble install asyncdispatch
# Встроено в stdlib (async)

# Тестирование
nimble install unittest
# Встроено в stdlib (unittest)

# Утилиты
nimble install chronos      # Время и дата
nimble install regex        # Регулярные выражения
nimble install docopt       # CLI аргументы
nimble install logging      # Логирование
nimble install yaml         # YAML парсинг
nimble install toml         # TOML парсинг

# Web фреймворки
nimble install jester       # Web framework
nimble install karax        # Frontend framework

================================================================================
                         КОНЕЦ README_NIM
================================================================================
