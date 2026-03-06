================================================================================
                    CUE - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Configuration + Validation + Declarative + Google
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка CUE
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые библиотеки

================================================================================
1. УСТАНОВКА CUE
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    CUE = CONFIGURATION + VALIDATION                          │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  CUE используется:                                                           │
│  • Configuration management                                                 │
│  • Data validation                                                          │
│  • Kubernetes manifests                                                     │
│  • Terraform configs                                                        │
│  • CI/CD validation                                                         │
│  • Policy enforcement                                                       │
│                                                                              │
│  • 2018+ разработка                                                         │
│  • Написан на Go                                                            │
│  • Google project                                                           │
│  • CNCF project                                                             │
│  • Declarative language                                                     │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Вариант 1: Через snap
sudo snap install cue --classic

# Вариант 2: Через binary release
curl -L -o cue.tar.gz https://github.com/cue-lang/cue/releases/latest/download/cue_v0.6.0_linux_amd64.tar.gz
tar -xzf cue.tar.gz
sudo mv cue /usr/local/bin/

# Вариант 3: Через Go
go install cuelang.org/cmd/cue@latest

# Проверка
cue version

macOS (Homebrew):
-----------------
brew install cue-lang/tap/cue

# Проверка
cue version

Windows:
--------
# Скачать с https://github.com/cue-lang/cue/releases
# Распаковать архив
# Добавить в PATH

# Проверка в PowerShell:
cue version

Docker (универсально):
----------------------
docker run -it --rm cuelang/cue cue version

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для CUE                                             │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ VS Code         │ ★★★★★ - С CUE extension (официальный)                     │
│ Vim/Neovim      │ ★★★★☆ - С cue.vim                                          │
│ Emacs           │ ★★★★☆ - С cue-mode                                           │
│ GoLand          │ ★★★★☆ - С CUE plugin                                         │
│ Текстовый + CLI │ ★★★★★ - Встроенный CLI                                     │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка VS Code + CUE:
------------------------
1. Extensions (Ctrl+Shift+X)
2. Установить: "CUE" от CUE Language
3. Автоматическая настройка

Установка CUE formatter:
------------------------
cue fmt file.cue  # Форматирование

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# CUE REPL (нет REPL, evaluation только)
# CUE оценивается напрямую

# Создание проекта
mkdir my_project && cd my_project

# Структура проекта:
my_project/
├── config.cue     # Конфигурация
├── schema.cue     # Схема валидации
└── README.md      # Документация

# Простая конфигурация (config.cue)
name: "John"
age: 25
city: "NYC"

# Валидация
cue vet config.cue

# Export в JSON
cue export config.cue --out json

# Export в YAML
cue export config.cue --out yaml

# Evaluation
cue eval config.cue

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ
================================================================================

# CUE использует module system

# cue.mod/module.cue файл:
module: "example.com/myproject"

# Import других файлов
import "example.com/myproject/schema"

# Поиск пакетов:
# https://github.com/cue-lang
# https://cuelang.org/

# Standard library:
# encoding/json
# encoding/yaml
# list
# math
# regexp
# string

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: Go требуется (для установки через go)
   cue install через go требует Go
   
   Решение:
   Использовать binary release
   Или установить Go сначала

⚠️ Проблема 2: Меньше библиотек
   Экосистема меньше чем YAML/JSON
   
   Решение:
   Использовать export в JSON/YAML
   Интегрировать с существующими tools

⚠️ Проблема 3: Документация
   Документация ещё развивается
   
   Решение:
   Читать cuelang.org
   Присоединиться к Discord

⚠️ Проблема 4: IDE поддержка
   Ограниченная поддержка
   
   Решение:
   Использовать VS Code + CUE extension
   Или текстовый редактор + CLI

⚠️ Проблема 5: Learning curve
   Концепция unification новая
   
   Решение:
   Читать tutorial на cuelang.org
   Практиковаться с примерами

⚠️ Проблема 6: Breaking changes
   Язык быстро развивается (до v1.0)
   
   Решение:
   Использовать specific versions
   Следить за changelog

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias cue='cue'" >> ~/.bashrc
echo "alias cue='cue'" >> ~/.zshrc

echo "alias cuevet='cue vet'" >> ~/.bashrc
echo "alias cuevet='cue vet'" >> ~/.zshrc

echo "alias cueeval='cue eval'" >> ~/.bashrc
echo "alias cueeval='cue eval'" >> ~/.zshrc

echo "alias cuefmt='cue fmt'" >> ~/.bashrc
echo "alias cuefmt='cue fmt'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия CUE
cue version

# Тест 2: Простая evaluation
echo 'name: "John"' | cue eval -

# Тест 3: Валидация
echo 'name: "John"
age: 25' > test.cue
cue vet test.cue
rm test.cue

# Тест 4: Export в JSON
echo 'name: "John"' | cue export - --out json

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ БИБЛИОТЕКИ
================================================================================

# Базовые библиотеки:

# Standard library:
# - encoding/json (JSON encoding/decoding)
# - encoding/yaml (YAML encoding/decoding)
# - list (list operations)
# - math (mathematical functions)
# - regexp (regular expressions)
# - string (string operations)

# Community packages:
# - Kubernetes schemas
# - Terraform schemas
# - Docker schemas

# FFI:
# - Go integration (встроенная)
# - JSON/YAML import/export

================================================================================
                         КОНЕЦ README_CUE
================================================================================
