================================================================================
                    LFE - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Lisp Syntax + Erlang VM + Concurrency + Distributed
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка LFE (rebar3)
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами (rebar3)
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые библиотеки

================================================================================
1. УСТАНОВКА LFE
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    LFE = LISP SYNTAX + ERLANG VM (BEAM)                      │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  LFE используется:                                                           │
│  • Distributed systems                                                      │
│  • Concurrent programming                                                   │
│  • Fault-tolerant systems                                                   │
│  • Telecom applications                                                     │
│  • Hot code reloading                                                       │
│                                                                              │
│  • Lisp синтаксис на Erlang VM                                              │
│  • 10+ лет развития (2008-2024)                                             │
│  • OTP совместимость                                                        │
│  • Actor model (processes, message passing)                                 │
│  • Let it crash philosophy                                                  │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Шаг 1: Установить Erlang/OTP
wget https://packages.erlang-solutions.com/erlang-solutions_2.0_all.deb
sudo dpkg -i erlang-solutions_2.0_all.deb
sudo apt update
sudo apt install erlang

# Шаг 2: Установить rebar3
wget https://s3.amazonaws.com/rebar3/rebar3
chmod +x rebar3
sudo mv rebar3 /usr/local/bin/

# Шаг 3: Установить LFE
rebar3 new lfe my_project

# Проверка
erl --version
rebar3 --version
lfe --version  # В REPL

macOS (Homebrew):
-----------------
brew install erlang
brew install rebar3

# Проверка
erl --version
rebar3 --version

Windows:
--------
# Через WSL (рекомендуется)
# Или установить Erlang с https://www.erlang.org/downloads

# Проверка в PowerShell:
erl --version

Docker (универсально):
----------------------
docker run -it --rm lfe/lfe lfe

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для LFE                                             │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ Emacs           │ ★★★★★ - С alferov-mode (лучшая поддержка)                 │
│ VS Code         │ ★★★★☆ - С lfe extension                                   │
│ Vim/Neovim      │ ★★★★☆ - С lfe.vim                                         │
│ IntelliJ        │ ★★★☆☆ - С Erlang plugin                                   │
│ Teko            │ ★★★☆☆ - Специализированный LFE editor                     │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка Emacs + alferov-mode:
-------------------------------
# Через MELPA:
M-x package-install RET alferov-mode RET

# Настройка:
(add-to-list 'auto-mode-alist '("\\.lfe$" . alferov-mode))

Установка VS Code + LFE:
------------------------
1. Extensions (Ctrl+Shift+X)
2. Установить: "LFE" от Robert Virding
3. Установить: "Erlang" от erlang-ls

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# LFE REPL
lfe

# В REPL:
lfe> (+ 2 2)
4
lfe> (exit)  # Выход

# Создание проекта
rebar3 new lfe my_project
cd my_project

# Структура проекта:
my_project/
├── rebar.config       # Конфигурация
├── src/               # Исходный код
│   └── my_project.lfe
├── test/              # Тесты
└── _build/            # Сборка

# Простая программа (src/my_project.lfe)
(defmodule my_project
  (export all))

(defun main (args)
  (io:format "Hello, LFE!~n"))

# Запуск
rebar3 lfe repl
rebar3 run

# Компиляция
rebar3 compile

# Hot code reloading
c(my_project).  # В REPL

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ (REBAR3)
================================================================================

# rebar.config файл:
{erl_opts, [debug_info]}.
{deps, []}.

{lfe_doc, [
  {docskel, "docskel"}
]}.

{lfe_lint, {files, ["src"]}}.

# Популярные пакеты:
# - lunit (testing)
# - lfe-doc (documentation)
# - clj (Clojure-like macros)
# - lfe-interop (Java interop)

# Установка зависимостей
rebar3 get-deps

# Компиляция
rebar3 compile

# Запуск с зависимостями
rebar3 lfe repl

# Публикация пакета
rebar3 hex publish

# Hex.pm (пакетный менеджер)
# https://hex.pm/

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: Erlang версия
   LFE требует Erlang/OTP 20+
   
   Решение:
   erl --version
   Установить последнюю версию

⚠️ Проблема 2: rebar3 не найден
   rebar3: command not found
   
   Решение:
   export PATH=$PATH:/usr/local/bin
   Или скопировать в ~/.local/bin

⚠️ Проблема 3: LFE REPL не запускается
   lfe: command not found
   
   Решение:
   rebar3 lfe repl  # Через rebar3

⚠️ Проблема 4: Конфликты зависимостей
   Разные версии библиотек
   
   Решение:
   rebar3 tree  # Показать дерево зависимостей
   Использовать rebar.lock

⚠️ Проблема 5: Hot code reloading не работает
   Код не обновляется
   
   Решение:
   c(module_name).  # В REPL
   Или использовать releases

⚠️ Проблема 6: Unicode проблемы
   Кириллица не отображается
   
   Решение:
   io:format("~ts~n", ["привет"]).  # ~ts для Unicode

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias lfe='rebar3 lfe repl'" >> ~/.bashrc
echo "alias lfe='rebar3 lfe repl'" >> ~/.zshrc

echo "alias lferun='rebar3 run'" >> ~/.bashrc
echo "alias lferun='rebar3 run'" >> ~/.zshrc

echo "alias lfecompile='rebar3 compile'" >> ~/.bashrc
echo "alias lfecompile='rebar3 compile'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия Erlang
erl --version

# Тест 2: Версия rebar3
rebar3 --version

# Тест 3: Простое вычисление
echo "(+ 2 2)" | rebar3 lfe repl

# Тест 4: Создание проекта
rebar3 new lfe test_project
cd test_project
rebar3 compile
cd ..
rm -rf test_project

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ БИБЛИОТЕКИ
================================================================================

# Базовые библиотеки (rebar.config):

# Testing
{deps, [
  {lunit, ".*", {git, "https://github.com/rvirding/lunit.git", {branch, "master"}}}
]}.

# Documentation
{deps, [
  {lfe_doc, ".*", {git, "https://github.com/lfe-docs/lfe_doc.git", {branch, "master"}}}
]}.

# Utilities
{deps, [
  {clj, ".*", {git, "https://github.com/rvirding/clj.git", {branch, "master"}}}
]}.

# HTTP client
{deps, [
  {hackney, ".*", {git, "https://github.com/benoitc/hackney.git", {branch, "master"}}}
]}.

# JSON
{deps, [
  {jsx, ".*", {git, "https://github.com/talentdeficit/jsx.git", {branch, "master"}}}
]}.

================================================================================
                         КОНЕЦ README_LFE
================================================================================
