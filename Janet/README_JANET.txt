================================================================================
                    JANET - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Современный Lisp + Встраиваемый + Практичный
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка Janet
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами (JPM)
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые библиотеки

================================================================================
1. УСТАНОВКА JANET
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    JANET = СОВРЕМЕННЫЙ LISP + 2017+                          │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  Janet используется:                                                         │
│  • Встраиваемые системы (как Lua, но Lisp)                                  │
│  • Скрипты и автоматизация                                                  │
│  • Конфигурационные файлы                                                   │
│  • Веб-разработка (Web frameworks)                                          │
│  • Компилируется в C                                                        │
│                                                                              │
│  • Маленький footprint (~500 KB)                                            │
│  • Быстрый (C реализация)                                                   │
│  • Функциональное программирование                                          │
│  • Garbage collected                                                        │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Вариант 1: Через пакетный менеджер
sudo apt update
sudo apt install janet

# Вариант 2: Из исходников (рекомендуется!)
git clone https://github.com/janet-lang/janet.git
cd janet
make
sudo make install

# Вариант 3: Через ночные сборки (nightly)
git clone https://github.com/janet-lang/janet.git
cd janet
git checkout master  # Nightly builds
make
sudo make install

# Проверка
janet --version

macOS (Homebrew):
-----------------
brew install janet

# Проверка
janet --version

Windows:
--------
# Скачать с https://github.com/janet-lang/janet/releases
# Или собрать из исходников через MinGW

# Проверка в PowerShell:
janet --version

Docker (универсально):
----------------------
docker run -it --rm janetlang/janet janet --version

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для Janet                                           │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ VS Code         │ ★★★★★ - С Janet extension (официальный)                   │
│ Emacs           │ ★★★★★ - С janet-mode (отличная поддержка)                 │
│ Vim/Neovim      │ ★★★★☆ - С janet.vim                                       │
│ Sublime Text    │ ★★★☆☆ - С Janet package                                   │
│ REPL            │ ★★★★☆ - Встроенный REPL                                     │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка VS Code + Janet:
--------------------------
1. Extensions (Ctrl+Shift+X)
2. Установить: "Janet" от Janet Language
3. Установить: "Janet Debugger" для отладки

Установка Emacs + janet-mode:
-----------------------------
# Через MELPA:
M-x package-install RET janet-mode RET

# Или вручную:
git clone https://github.com/janet-lang/janet-mode.git
# Добавить в ~/.emacs

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# Janet REPL
janet

# В REPL:
repl:1:> (print "Hello, Janet!")
repl:2:> (+ 2 2)
4
repl:3:> (os/exit)  # Выход

# Запуск скрипта
janet script.janet

# Компиляция в байт-код
janet -c script.janet  # Создаёт script.jimage

# Запуск байт-кода
janet script.jimage

# Проверка синтаксиса
janet -e '(print "OK")'

# Создание проекта
mkdir my_project && cd my_project
# Janet не требует сложной структуры

# Структура проекта:
my_project/
├── main.janet       # Главный файл
├── modules/         # Модули
│   └── utils.janet
├── test/            # Тесты
└── project.janet    # Конфигурация проекта

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ (JPM)
================================================================================

# JPM = Janet Package Manager

# Инициализация проекта
jpm init

# Структура project.janet:
(name "my-project")
(version "0.1.0")
(description "My Janet project")
(author "Your Name")

(dependencies
  ["https://github.com/janet-lang/http" :tag "v1.0.0"])

# Установка зависимостей
jpm deps

# Запуск проекта
jpm run

# Тесты
jpm test

# Установка глобального пакета
jpm install package_name

# Поиск пакетов
# https://github.com/janet-lang/janet-packages

# Сообщество пакеты:
# https://github.com/janet-lang

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: Nightly builds нестабильны
   Мастер ветка может ломаться
   
   Решение: Использовать стабильные релизы
   git checkout v1.32.0  # Стабильная версия

⚠️ Проблема 2: JPM не находит пакеты
   package not found
   
   Решение:
   Проверить project.janet зависимости
   jpm deps --force

⚠️ Проблема 3: C компилятор не найден
   Janet требует GCC/Clang для сборки
   
   Решение:
   sudo apt install build-essential

⚠️ Проблема 4: Path проблемы
   janet: command not found
   
   Решение:
   export PATH="/usr/local/bin:$PATH"
   Добавить в ~/.bashrc

⚠️ Проблема 5: Encoding проблемы
   Кириллица не отображается
   
   Решение:
   Janet поддерживает UTF-8 по умолчанию
   Проверить locale настройки

⚠️ Проблема 6: Старая версия в репозиториях
   apt install janet может установить старую
   
   Решение:
   Собрать из исходников для последней версии

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias j='janet'" >> ~/.bashrc
echo "alias j='janet'" >> ~/.zshrc

echo "alias jr='jpm run'" >> ~/.bashrc
echo "alias jr='jpm run'" >> ~/.zshrc

echo "alias jt='jpm test'" >> ~/.bashrc
echo "alias jt='jpm test'" >> ~/.zshrc

echo "alias jd='jpm deps'" >> ~/.bashrc
echo "alias jd='jpm deps'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия Janet
janet --version

# Тест 2: Простое вычисление
echo "(+ 2 2)" | janet

# Тест 3: Запуск скрипта
echo '(print "OK")' > test.janet
janet test.janet
rm test.janet

# Тест 4: JPM
jpm --version
jpm init test_project
cd test_project
jpm deps
cd ..
rm -rf test_project

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ БИБЛИОТЕКИ
================================================================================

# Базовые пакеты (jpm install):

# HTTP клиент
jpm install https://github.com/janet-lang/http

# JSON
jpm install https://github.com/janet-lang/json

# Дата и время
# Встроено в os/ модуль

# Тестирование
# Встроено в jpm test

# Веб фреймворк
jpm install https://github.com/janet-lang/web

# Утилиты
jpm install https://github.com/janet-lang/bytes
jpm install https://github.com/janet-lang/fiber

# Базы данных
jpm install https://github.com/janet-lang/sqlite3

# Криптография
jpm install https://github.com/janet-lang/crypto

================================================================================
                         КОНЕЦ README_JANET
================================================================================
