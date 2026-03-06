================================================================================
                    CARBON - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         C++ Successor + Interoperability + Modern Syntax
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка Carbon
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые библиотеки

================================================================================
1. УСТАНОВКА CARBON
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    CARBON = C++ SUCCESSOR + INTEROPERABILITY                 │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  Carbon используется:                                                        │
│  • C++ migration                                                            │
│  • Systems programming                                                      │
│  • Performance-critical applications                                        │
│  • Когда нужен C++ но современнее                                           │
│  • Early adoption                                                           │
│                                                                              │
│  • 2022+ разработка (очень новый)                                           │
│  • Google project                                                           │
│  • Open source (GitHub)                                                     │
│  • C++ интероперабельность                                                  │
│  • LLVM backend                                                             │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Вариант 1: Через Bazel
git clone https://github.com/carbon-language/carbon-lang.git
cd carbon-lang
bazel run //installer

# Вариант 2: Через Docker
docker run -it --rm ghcr.io/carbon-language/carbon-lang carbon

# Проверка
carbon --version

macOS:
------
# Через Bazel
git clone https://github.com/carbon-language/carbon-lang.git
cd carbon-lang
bazel run //installer

# Проверка
carbon --version

Windows:
--------
# Через WSL (рекомендуется)
# Или через Docker

# Проверка в PowerShell:
carbon --version

Docker (универсально):
----------------------
docker run -it --rm ghcr.io/carbon-language/carbon-lang carbon --version

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для Carbon                                          │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ VS Code         │ ★★★★☆ - С Carbon extension (experimental)                 │
│ Vim/Neovim      │ ★★★☆☆ - С carbon.vim (experimental)                       │
│ Emacs           │ ★★★☆☆ - С carbon-mode (experimental)                      │
│ Bazel           │ ★★★★★ - Официальная сборка                                │
│ Текстовый + CLI │ ★★★★★ - Встроенный компилятор                             │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка VS Code + Carbon:
---------------------------
1. Extensions (Ctrl+Shift+X)
2. Установить: "Carbon" от Carbon Language
3. Экспериментальная поддержка

Установка Bazel:
----------------
# Требуется для сборки Carbon
sudo apt install bazel

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# Carbon REPL
carbon repl

# В REPL:
carbon> fn Add(a: i32, b: i32) -> i32 { return a + b; }
carbon> Add(2, 3)
5

# Создание проекта
mkdir my_project && cd my_project

# Структура проекта:
my_project/
├── main.carbon      # Главный файл
├── BUILD.bazel      # Bazel build file
└── README.md        # Документация

# Простая программа (main.carbon)
package MyProject api;

fn Main() -> i32 {
  Print("Hello, Carbon!");
  return 0;
}

# Компиляция
bazel build //:main

# Запуск
bazel run //:main

# Форматирование
carbon fmt main.carbon

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ
================================================================================

# Carbon использует Bazel для сборки

# BUILD.bazel файл:
load("@rules_carbon//carbon:defs.bzl", "carbon_binary")

carbon_binary(
    name = "main",
    srcs = ["main.carbon"],
)

# Популярные пакеты:
# - rules_carbon (Bazel rules)
# - Carbon standard library
# - C++ interop libraries

# Установка зависимостей
# Через Bazel WORKSPACE

# Поиск пакетов
# https://github.com/carbon-language/carbon-lang

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: Очень новый язык
   Carbon в активной разработке (experimental)
   
   Решение:
   Следить за обновлениями
   Использовать nightly builds

⚠️ Проблема 2: Требуется Bazel
   Bazel может быть сложным для установки
   
   Решение:
   Использовать Docker образ
   Или установить Bazel через apt

⚠️ Проблема 3: Меньше библиотек
   Экосистема только формируется
   
   Решение:
   Использовать C++ библиотеки через interop
   Писать свои библиотеки

⚠️ Проблема 4: Документация
   Документация ещё развивается
   
   Решение:
   Читать carbon-language.org
   Присоединиться к Discord

⚠️ Проблема 5: IDE поддержка
   Экспериментальная поддержка
   
   Решение:
   Использовать VS Code + Carbon extension
   Или текстовый редактор + CLI

⚠️ Проблема 6: Breaking changes
   Язык быстро развивается
   
   Решение:
   Использовать specific commits
   Следить за changelog

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias carbon='carbon'" >> ~/.bashrc
echo "alias carbon='carbon'" >> ~/.zshrc

echo "alias carbonrun='bazel run'" >> ~/.bashrc
echo "alias carbonrun='bazel run'" >> ~/.zshrc

echo "alias carbonbuild='bazel build'" >> ~/.bashrc
echo "alias carbonbuild='bazel build'" >> ~/.zshrc

echo "alias carbonfmt='carbon fmt'" >> ~/.bashrc
echo "alias carbonfmt='carbon fmt'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия Carbon
carbon --version

# Тест 2: Простое вычисление
echo "fn Main() -> i32 { return 2 + 2; }" | carbon repl

# Тест 3: Создание проекта
mkdir test_project && cd test_project
# Создать main.carbon
# Создать BUILD.bazel
bazel run //:main
cd ..
rm -rf test_project

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ БИБЛИОТЕКИ
================================================================================

# Базовые библиотеки:

# Official packages:
# - rules_carbon (Bazel rules)
# - Carbon standard library
# - C++ interop

# Community packages:
# - В разработке

# FFI:
# - C++ interop (встроенная)
# - C interop (через C++)

================================================================================
                         КОНЕЦ README_CARBON
================================================================================
