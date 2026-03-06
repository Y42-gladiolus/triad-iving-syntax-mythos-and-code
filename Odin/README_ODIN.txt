================================================================================
                    ODIN - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Modern Systems + Explicit + Performance + Simplicity
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка Odin
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые библиотеки

================================================================================
1. УСТАНОВКА ODIN
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    ODIN = MODERN SYSTEMS + EXPLICIT + FAST                   │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  Odin используется:                                                          │
│  • Game development                                                         │
│  • Systems programming                                                      │
│  • Performance-critical applications                                        │
│  • Data-oriented design                                                     │
│  • Когда нужен C но современнее                                             │
│                                                                              │
│  • 2016+ разработка                                                         │
│  • Написан на Odin (self-hosted)                                            │
│  • Нет garbage collector                                                    │
│  • LLVM backend                                                             │
│  • Explicit design                                                          │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Вариант 1: Через официальный скрипт
curl -L https://github.com/odin-lang/Odin/releases/latest/download/odin-linux-amd64-latest.tar.gz | tar -xz
sudo mv odin /usr/local/bin/

# Вариант 2: Из исходников
git clone https://github.com/odin-lang/Odin.git
cd Odin
./build.sh
sudo cp odin /usr/local/bin/

# Проверка
odin version

macOS (Homebrew):
-----------------
brew install odin

# Проверка
odin version

Windows:
--------
# Скачать с https://github.com/odin-lang/Odin/releases
# Распаковать архив
# Добавить в PATH

# Проверка в PowerShell:
odin version

Docker (универсально):
----------------------
# Нет официального образа
# Создать свой Dockerfile

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для Odin                                            │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ VS Code         │ ★★★★★ - С Odin extension (официальный)                    │
│ Vim/Neovim      │ ★★★★☆ - С odin.vim                                         │
│ Emacs           │ ★★★★☆ - С odin-mode                                          │
│ Zed             │ ★★★★☆ - Встроенная поддержка                               │
│ Текстовый + CLI │ ★★★★★ - Встроенный компилятор                             │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка VS Code + Odin:
-------------------------
1. Extensions (Ctrl+Shift+X)
2. Установить: "Odin" от Odin Language
3. Автоматическая настройка

Установка Odin formatter:
-------------------------
odin fmt file.odin  # Форматирование

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# Odin REPL (нет REPL, компиляция только)
# Odin компилируется напрямую

# Создание проекта
mkdir my_project && cd my_project

# Структура проекта:
my_project/
├── main.odin      # Главный файл
├── build.odin     # Build script
└── README.md      # Документация

# Простая программа (main.odin)
package main

import "core:fmt"

main :: proc() {
  fmt.println("Hello, Odin!")
}

# Компиляция
odin build .

# Запуск
./my_project

# Compile and run
odin run main.odin

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ
================================================================================

# Odin не имеет пакетного менеджера (пока)

# Использование сторонних библиотек:
# Clone repository
git clone https://github.com/odin-lang/odin-core

# Add to project
# Manual dependency management

# Поиск пакетов:
# https://github.com/odin-lang
# https://pkg.odin-lang.org/

# Standard library:
# core:fmt (formatting)
# core:os (OS operations)
# core:io (I/O operations)
# core:math (mathematical functions)

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: Beta статус
   Odin в активной разработке (не 1.0 ещё)
   
   Решение:
   Следить за обновлениями
   Использовать latest release

⚠️ Проблема 2: Меньше библиотек
   Экосистема только формируется
   
   Решение:
   Использовать C interop
   Писать свои библиотеки

⚠️ Проблема 3: Документация
   Документация ещё развивается
   
   Решение:
   Читать odin-lang.org
   Присоединиться к Discord

⚠️ Проблема 4: IDE поддержка
   Ограниченная поддержка
   
   Решение:
   Использовать VS Code + Odin extension
   Или текстовый редактор + CLI

⚠️ Проблема 5: Нет package manager
   Manual dependency management
   
   Решение:
   Clone repositories manually
   Follow project updates

⚠️ Проблема 6: Breaking changes
   Язык быстро развивается
   
   Решение:
   Использовать specific releases
   Следить за changelog

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias odin='odin'" >> ~/.bashrc
echo "alias odin='odin'" >> ~/.zshrc

echo "alias odinrun='odin run'" >> ~/.bashrc
echo "alias odinrun='odin run'" >> ~/.zshrc

echo "alias odinbuild='odin build'" >> ~/.bashrc
echo "alias odinbuild='odin build'" >> ~/.zshrc

echo "alias odinfmt='odin fmt'" >> ~/.bashrc
echo "alias odinfmt='odin fmt'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия Odin
odin version

# Тест 2: Простая программа
echo 'package main
import "core:fmt"
main :: proc() { fmt.println("OK") }' > test.odin
odin run test.odin
rm test.odin

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ БИБЛИОТЕКИ
================================================================================

# Базовые библиотеки:

# Standard library:
# - core:fmt (formatting)
# - core:os (OS operations)
# - core:io (I/O operations)
# - core:math (mathematical functions)
# - core:mem (memory operations)
# - core:strings (string operations)

# Community packages:
# - В разработке

# FFI:
# - C interop (встроенная)
# - Foreign procedure interface

================================================================================
                         КОНЕЦ README_ODIN
================================================================================
