================================================================================
                    CLOJURE - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Modern Lisp + JVM + Functional + Immutability
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка Clojure (leiningen/deps)
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами (Leiningen/deps)
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые библиотеки

================================================================================
1. УСТАНОВКА CLOJURE
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    CLOJURE = MODERN LISP + JVM + FUNCTIONAL                  │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  Clojure используется:                                                       │
│  • Web development (Ring, Compojure)                                        │
│  • Data processing                                                          │
│  • Functional programming на JVM                                            │
│  • Distributed systems                                                      │
│  • Scripting и automation                                                   │
│                                                                              │
│  • Работает на JVM (и ClojureScript для JS)                                 │
│  • 15+ лет развития (2007-2024)                                             │
│  • Функциональное программирование                                          │
│  • Immutable data structures                                                │
│  • Homoiconicity (код как данные)                                           │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Через deps.clj (рекомендуется!)
curl -O https://download.clojure.org/install/linux-install-1.11.1.1262.sh
chmod +x linux-install-1.11.1.1262.sh
sudo ./linux-install-1.11.1.1262.sh

# Или через Leiningen
wget https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein
chmod +x lein
sudo mv lein /usr/local/bin/
lein

# Проверка
clojure --version
lein --version

macOS (Homebrew):
-----------------
brew install clojure
brew install leiningen

# Проверка
clojure --version

Windows:
--------
# Через Chocolatey
choco install clojure

# Или Leiningen
# Скачать с https://leiningen.org/

# Проверка в PowerShell:
clojure --version

Docker (универсально):
----------------------
docker run -it --rm clojure clojure --version

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для Clojure                                         │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ VS Code         │ ★★★★★ - С Calva extension (лучшая поддержка)              │
│ IntelliJ IDEA   │ ★★★★★ - С Cursive plugin (платный)                        │
│ Emacs           │ ★★★★★ - С CIDER (лучшая для Lisp)                         │
│ Vim/Neovim      │ ★★★★☆ - С fireplace.vim                                    │
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
(add-hook 'clojure-mode-hook #'cider-mode)

Установка Leiningen:
--------------------
wget https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein
chmod +x lein
sudo mv lein /usr/local/bin/

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# Clojure REPL
clojure

# В REPL:
user=> (+ 2 2)
4
user=> (exit)  # Выход

# Leiningen REPL
lein repl

# Создание проекта
lein new app my-project
cd my-project

# Структура проекта:
my-project/
├── project.clj        # Leiningen конфигурация
├── src/
│   └── my_project/
│       └── core.clj   # Главный файл
├── test/
│   └── my_project/
│       └── core_test.clj
└── README.md

#deps.edn проект (современный)
clojure -M -m my-project.core

# Запуск проекта
lein run
clojure -M -m my-project.core

# Компиляция в JAR
lein uberjar

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ (LEININGEN/DEPS)
================================================================================

# Leiningen (project.clj)
:dependencies [[org.clojure/clojure "1.11.0"]
               [ring/ring-core "1.9.0"]
               [compojure "1.6.0"]]

# deps.edn (современный)
{:deps {org.clojure/clojure {:mvn/version "1.11.0"}
        ring/ring-core {:mvn/version "1.9.0"}}}

# Установка зависимостей
lein deps
clojure -M

# Поиск пакетов
# https://clojars.org/
# https://deps.edn/

# Популярные библиотеки:
# ring (web)
# compojure (routing)
# core.async (async)
# spec (specification)
# test.check (testing)

# Запуск с зависимостями
lein run
clojure -M -m my-project.core

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: Java версия
   Clojure требует JDK 8+
   
   Решение:
   java -version
   export JAVA_HOME=/usr/lib/jvm/java-11-openjdk

⚠️ Проблема 2: Leiningen медленный первый запуск
   Первый запуск загружает зависимости
   
   Решение:
   Это нормально - последующие запуски быстрее
   Использовать deps.edn для новых проектов

⚠️ Проблема 3: Clojure vs ClojureScript
   Clojure (JVM) vs ClojureScript (JS)
   
   Решение:
   Clojure для JVM приложений
   ClojureScript для веб/браузер

⚠️ Проблема 4: Память JVM
   Leiningen может потреблять много памяти
   
   Решение:
   export LEIN_JVM_OPTS="-Xmx2G"
   Добавить в ~/.leinrc

⚠️ Проблема 5: Конфликты зависимостей
   Разные версии библиотек
   
   Решение:
   lein deps :tree
   Использовать exclusions

⚠️ Проблема 6: Compile time
   Clojure компиляция может быть медленной
   
   Решение:
   Использовать AOT компиляцию
   lein compile

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias clj='clojure'" >> ~/.bashrc
echo "alias clj='clojure'" >> ~/.zshrc

echo "alias lein='lein'" >> ~/.bashrc
echo "alias lein='lein'" >> ~/.zshrc

echo "alias cljr='lein repl'" >> ~/.bashrc
echo "alias cljr='lein repl'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия Clojure
clojure --version

# Тест 2: Версия Leiningen
lein --version

# Тест 3: Простое вычисление
echo "(+ 2 2)" | clojure

# Тест 4: Leiningen проект
lein new app test_project
cd test_project
lein run
cd ..
rm -rf test_project

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ БИБЛИОТЕКИ
================================================================================

# Базовые библиотеки (project.clj):

# Web
[ring/ring-core "1.9.0"]
[compojure "1.6.0"]
[ring/ring-jetty-adapter "1.9.0"]

# Functional
[org.clojure/core.async "1.6.673"]

# Testing
[org.clojure/test.check "1.1.1"]

# Data processing
[org.clojure/data.json "2.4.0"]

# Database
[org.clojure/java.jdbc "0.7.12"]
[hikari-cp "2.13.0"]

# Logging
[org.clojure/tools.logging "1.2.4"]

# Spec
[org.clojure/spec.alpha "0.3.218"]

================================================================================
                         КОНЕЦ README_CLOJURE
================================================================================
