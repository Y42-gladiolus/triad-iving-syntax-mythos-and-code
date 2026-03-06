================================================================================
                    CLOJURESCRIPT - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Lisp + JavaScript Target + Functional Programming
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка ClojureScript (Leiningen/deps)
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые библиотеки

================================================================================
1. УСТАНОВКА CLOJURESCRIPT
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    CLOJURESCRIPT = LISP + JAVASCRIPT                         │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  ClojureScript используется:                                                 │
│  • Веб-разработка (frontend)                                                │
│  • Node.js приложения                                                       │
│  • React приложения (Reagent, Re-frame)                                     │
│  • Функциональное программирование на JS                                    │
│  • Mobile приложения (React Native)                                         │
│                                                                              │
│  • Компилируется в JavaScript                                               │
│  • Lisp синтаксис (S-выражения)                                             │
│  • Immutable по умолчанию                                                   │
│  • 10+ лет развития (2011-2024)                                             │
│  • Отличная JavaScript интероперабельность                                  │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Вариант 1: Через Leiningen (рекомендуется!)
wget https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein
chmod +x lein
sudo mv lein /usr/local/bin/
lein

# Вариант 2: Через deps.edn (Clojure CLI)
curl -O https://download.clojure.org/install/linux-install-1.11.1.1262.sh
chmod +x linux-install-1.11.1.1262.sh
sudo ./linux-install-1.11.1.1262.sh

# Проверка
lein --version
clj --version

macOS (Homebrew):
-----------------
brew install leiningen
brew install clojure

# Проверка
lein --version

Windows:
--------
# Скачать Leiningen с https://leiningen.org/
# Установщик .bat
# Добавить в PATH

# Проверка в PowerShell:
lein --version

Docker (универсально):
----------------------
docker run -it --rm clojure lein --version

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для ClojureScript                                   │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ VS Code         │ ★★★★★ - С Calva extension (лучшая поддержка)              │
│ IntelliJ IDEA   │ ★★★★★ - С Cursive plugin (платный)                        │
│ Emacs           │ ★★★★★ - С CIDER (лучшая для Lisp)                         │
│ Vim/Neovim      │ ★★★★☆ - С fireplace.vim                                   │
│ Teko            │ ★★★☆☆ - Специализированный Clojure editor                 │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка VS Code + Calva:
--------------------------
1. Extensions (Ctrl+Shift+X)
2. Установить: "Calva" от Calva
3. Автоматическая настройка REPL

Установка Emacs + CIDER:
------------------------
# Через MELPA:
M-x package-install RET cider RET

# Настройка:
(add-hook 'clojurescript-mode-hook #'cider-mode)

Установка Leiningen + Figwheel:
-------------------------------
lein new reagent my-app
cd my-app
lein figwheel

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# ClojureScript REPL
lein repl

# В REPL:
cljs.user=> (+ 2 2)
4
cljs.user=> (exit)  # Выход

# Создание проекта
lein new reagent my-app
cd my-app

# Структура проекта:
my-app/
├── project.clj        # Конфигурация Leiningen
├── src/               # Исходный код
│   └── my_app/
│       └── core.cljs  # Главный файл
├── resources/         # Ресурсы
└── test/              # Тесты

# Запуск проекта
lein figwheel

# Сборка
lein build

# Компиляция в JavaScript
lein cljsbuild once

# Production сборка
lein cljsbuild once min

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ
================================================================================

# ClojureScript использует Leiningen (project.clj)

# project.clj зависимости:
:dependencies [[org.clojure/clojure "1.11.0"]
               [org.clojure/clojurescript "1.11.54"]
               [reagent "1.2.0"]
               [re-frame "1.3.0"]]

# Добавить пакет
lein deps

# Обновить пакеты
lein ancient
lein upgrade

# Clojure CLI (deps.edn):
{:deps {org.clojure/clojurescript {:mvn/version "1.11.54"}
        reagent {:mvn/version "1.2.0"}}}

# Поиск пакетов
# https://clojars.org/
# https://deps.edn/

# Локальные зависимости
:dependencies [[my-local-lib "1.0.0" :local/root "../my-lib"]]

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: Java требуется
   ClojureScript требует JDK 8+
   
   Решение:
   sudo apt install openjdk-11-jdk
   export JAVA_HOME=/usr/lib/jvm/java-11-openjdk

⚠️ Проблема 2: Leiningen медленный первый запуск
   Первый запуск загружает зависимости
   
   Решение:
   Это нормально - последующие запуски быстрее
   Использовать offline mode после первого раза

⚠️ Проблема 3: Figwheel не запускается
   Port занят или настройки неверны
   
   Решение:
   Проверить port в project.clj
   kill процесс на порту 3449

⚠️ Проблема 4: REPL не подключается
   NREPL не запускается
   
   Решение:
   Перезапустить Leiningen
   Проверить версию ClojureScript

⚠️ Проблема 5: JavaScript интероперабельность
   Сложности с JS библиотеками
   
   Решение:
   Использовать js/ префикс
   Читать CLJS JS interop guide

⚠️ Проблема 6: Сборка медленная
   ClojureScript компиляция долгая
   
   Решение:
   Использовать figwheel для hot reload
   Использовать production build только для релиза

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias clj='lein repl'" >> ~/.bashrc
echo "alias clj='lein repl'" >> ~/.zshrc

echo "alias cljb='lein cljsbuild'" >> ~/.bashrc
echo "alias cljb='lein cljsbuild'" >> ~/.zshrc

echo "alias cljf='lein figwheel'" >> ~/.bashrc
echo "alias cljf='lein figwheel'" >> ~/.zshrc

echo "alias cljt='lein test'" >> ~/.bashrc
echo "alias cljt='lein test'" >> ~/.zshrc

echo "alias cljc='lein clean'" >> ~/.bashrc
echo "alias cljc='lein clean'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия Leiningen
lein --version

# Тест 2: Версия ClojureScript
lein repl < <(echo "(cljs.core/+ 2 2)")

# Тест 3: Создание проекта
lein new reagent test_project
cd test_project
lein figwheel &
sleep 10
curl http://localhost:3449
cd ..
rm -rf test_project

# Тест 4: Простое вычисление
echo "(+ 2 2)" | lein repl

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ БИБЛИОТЕКИ
================================================================================

# Базовые пакеты (project.clj):

# Core
[org.clojure/clojurescript "1.11.54"]

# React integration
[reagent "1.2.0"]          # React wrapper
[re-frame "1.3.0"]         # Framework

# Routing
[reitit "0.6.0"]           # Routing library

# HTTP
[cljs-http "0.1.46"]       # HTTP client

# State management
[re-frame "1.3.0"]         # Already includes

# Testing
[olivergeary/cljs-test "0.1.0"]
[day8.re-frame/test "0.1.5"]

# Utilities
[cljsjs/google-analytics "0.1.0"]
[bidi "2.1.6"]             # URL routing

# Build tools
[lein-cljsbuild "1.1.8"]
[lein-figwheel "0.5.19"]

================================================================================
                         КОНЕЦ README_CLOJURESCRIPT
================================================================================
