================================================================================
                    CRYSTAL - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Ruby Syntax + C Performance + Static Typing
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка Crystal
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами (Shards)
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые библиотеки

================================================================================
1. УСТАНОВКА CRYSTAL
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    CRYSTAL = RUBY SYNTAX + C PERFORMANCE                     │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  Crystal используется:                                                       │
│  • Web development                                                          │
│  • CLI tools                                                                │
│  • API servers                                                              │
│  • Ruby migration                                                           │
│  • Performance-critical applications                                        │
│                                                                              │
│  • 2014+ разработка                                                         │
│  • Написан на Crystal (self-hosted)                                         │
│  • LLVM backend                                                             │
│  • Garbage collected                                                        │
│  • Ruby-like syntax                                                         │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Вариант 1: Через официальный репозиторий
curl -fsSL https://crystal-lang.org/install.sh | sudo bash

# Вариант 2: Через apt
sudo apt update
sudo apt install crystal

# Проверка
crystal --version
shards --version

macOS (Homebrew):
-----------------
brew install crystal

# Проверка
crystal --version

Windows:
--------
# Через WSL (рекомендуется)
# Или через Windows Subsystem (в разработке)

# Проверка в WSL:
crystal --version

Docker (универсально):
----------------------
docker run -it --rm crystallang/crystal crystal --version

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для Crystal                                         │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ VS Code         │ ★★★★★ - С Crystal extension (официальный)                 │
│ Vim/Neovim      │ ★★★★☆ - С crystal.vim                                      │
│ Emacs           │ ★★★★☆ - С crystal-mode                                       │
│ Atom            │ ★★★★☆ - С language-crystal                                 │
│ Teko            │ ★★★★☆ - Встроенная поддержка                               │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка VS Code + Crystal:
----------------------------
1. Extensions (Ctrl+Shift+X)
2. Установить: "Crystal" от Crystal Language
3. Автоматическая настройка

Установка Crystal formatter:
----------------------------
crystal tool format file.cr  # Форматирование

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# Crystal REPL
crystal play

# В REPL:
> puts 2 + 2
4
> exit  # Выход

# Создание проекта
crystal init app my_project
cd my_project

# Структура проекта:
my_project/
├── shard.yml        # Конфигурация проекта
├── src/             # Исходный код
│   └── my_project.cr
├── spec/            # Тесты
└── README.md        # Документация

# Простая программа (src/my_project.cr)
puts "Hello, Crystal!"

# Компиляция
crystal build src/my_project.cr

# Запуск
./my_project

# Compile and run
crystal run src/my_project.cr

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ (SHARDS)
================================================================================

# Shards (Crystal package manager)

# shard.yml файл:
name: my_project
version: 0.1.0

dependencies:
  http-client:
    github: crystal-lang/http-client
    version: ~> 0.1.0

# Установка зависимостей
shards install

# Обновление зависимостей
shards update

# Поиск пакетов:
# https://shards.info/
# https://github.com/crystal-lang

# Популярные пакеты:
# - kemal (web framework)
# - lucky (web framework)
# - ameba (linter)
# - spec (testing)

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: LLVM требуется
   Crystal требует LLVM для компиляции
   
   Решение:
   sudo apt install llvm
   Или использовать официальный installer

⚠️ Проблема 2: Медленная компиляция
   Первая компиляция может занять время
   
   Решение:
   Использовать crystal run для разработки
   Использовать --release для production

⚠️ Проблема 3: Windows support
   Windows support ещё в разработке
   
   Решение:
   Использовать WSL
   Или использовать Linux/macOS

⚠️ Проблема 4: Меньше библиотек
   Экосистема меньше чем Ruby/Python
   
   Решение:
   Использовать C bindings
   Писать свои библиотеки

⚠️ Проблема 5: GC паузы
   GC может вызывать паузы
   
   Решение:
   GC.disable для critical sections
   Оптимизировать memory usage

⚠️ Проблема 6: Breaking changes
   Язык быстро развивается (до 1.0)
   
   Решение:
   Использовать specific versions
   Следить за changelog

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias cr='crystal'" >> ~/.bashrc
echo "alias cr='crystal'" >> ~/.zshrc

echo "alias crrun='crystal run'" >> ~/.bashrc
echo "alias crrun='crystal run'" >> ~/.zshrc

echo "alias crbuild='crystal build'" >> ~/.bashrc
echo "alias crbuild='crystal build'" >> ~/.zshrc

echo "alias crfmt='crystal tool format'" >> ~/.bashrc
echo "alias crfmt='crystal tool format'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия Crystal
crystal --version

# Тест 2: Версия Shards
shards --version

# Тест 3: Простое вычисление
echo "puts 2 + 2" | crystal run -

# Тест 4: Создание проекта
crystal init app test_project
cd test_project
crystal run
cd ..
rm -rf test_project

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ БИБЛИОТЕКИ
================================================================================

# Базовые библиотеки:

# Web frameworks
# - Kemal (https://github.com/kemalcr/kemal)
# - Lucky (https://github.com/luckyframework/lucky)

# HTTP client
# - HTTP::Client (встроенный)

# Database
# - Crecto (ORM)
# - Jennifer (ORM)

# Testing
# - Spec (встроенный)

# Linting
# - Ameba (https://github.com/crystal-ameba/ameba)

# JSON/YAML
# - JSON (встроенный)
# - YAML (встроенный)

================================================================================
                         КОНЕЦ README_CRYSTAL
================================================================================
