================================================================================
                    HASKELL - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Pure Functional + Lazy Evaluation + Type Safety
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка Haskell (GHC/Cabal/Stack)
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами (Cabal/Stack)
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые библиотеки

================================================================================
1. УСТАНОВКА HASKELL
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    HASKELL = PURE FUNCTIONAL + TYPE SAFETY                   │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  Haskell используется:                                                       │
│  • Compilers и interpreters                                                 │
│  • Financial systems                                                        │
│  • Data analysis                                                            │
│  • Formal verification                                                      │
│  • Research и academia                                                      │
│                                                                              │
│  • 1990+ разработка                                                         │
│  • GHC (Glasgow Haskell Compiler)                                           │
│  • Pure functional programming                                              │
│  • Lazy evaluation                                                          │
│  • Strong static typing                                                     │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Вариант 1: Через ghcup (рекомендуется!)
curl --proto '=https' --tlsv1.2 -sSf https://get-ghcup.haskell.org | sh

# Вариант 2: Через apt (может быть старая версия)
sudo apt update
sudo apt install ghc cabal-install

# Проверка
ghc --version
cabal --version

macOS (Homebrew):
-----------------
brew install ghc cabal-install

# Или через ghcup
curl --proto '=https' --tlsv1.2 -sSf https://get-ghcup.haskell.org | sh

# Проверка
ghc --version

Windows:
--------
# Скачать с https://www.haskell.org/platform/
# Установщик .exe включает GHC и Cabal

# Проверка в PowerShell:
ghc --version

Docker (универсально):
----------------------
docker run -it --rm haskell:latest ghc --version

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для Haskell                                         │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ VS Code         │ ★★★★★ - С Haskell extension (официальный)                 │
│ IntelliJ IDEA   │ ★★★★★ - С Haskell plugin (JetBrains)                      │
│ Vim/Neovim      │ ★★★★☆ - С haskell-vim                                      │
│ Emacs           │ ★★★★★ - С haskell-mode + intero                             │
│ Teko            │ ★★★★☆ - Встроенная поддержка                               │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка VS Code + Haskell:
----------------------------
1. Extensions (Ctrl+Shift+X)
2. Установить: "Haskell" от Haskell Foundation
3. Установить: "Haskell Syntax Highlighting"
4. Автоматическая настройка

Установка Emacs + haskell-mode:
-------------------------------
# Через MELPA:
M-x package-install RET haskell-mode RET

Установка Stack:
----------------
curl -sSL https://get.haskellstack.org/ | sh

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# Haskell REPL (GHCi)
ghci

# В GHCi:
Prelude> 2 + 2
4
Prelude> :quit  # Выход

# Создание проекта
stack new my_project
cd my_project

# Структура проекта:
my_project/
├── stack.yaml     # Stack конфигурация
├── my_project.cabal  # Cabal файл
├── src/           # Исходный код
│   └── Main.hs
├── test/          # Тесты
└── README.md      # Документация

# Простая программа (src/Main.hs)
module Main where

main :: IO ()
main = putStrLn "Hello, Haskell!"

# Компиляция
stack build

# Запуск
stack run

# GHCi с файлом
ghci src/Main.hs

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ (CABAL/STACK)
================================================================================

# Cabal (traditional package manager)
cabal update
cabal install package_name
cabal build
cabal run

# Stack (modern package manager)
stack update
stack install package_name
stack build
stack run

# cabal файл:
name:          my-project
version:       0.1.0.0
build-type:    Simple

executable my-project
    main-is:          Main.hs
    build-depends:    base ^>=4.14
    hs-source-dirs:   src
    default-language: Haskell2010

# Stack файл:
resolver: lts-19.0
packages:
- .

# Поиск пакетов:
# https://hackage.haskell.org/
# https://www.stackage.org/

# Популярные пакеты:
# - lens (lenses)
# - aeson (JSON)
# - text (text processing)
# - vector (arrays)
# - async (concurrency)

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: GHC версии
   Разные пакеты требуют разные версии GHC
   
   Решение:
   Используйте stack (управляет версиями)
   Или ghcup для управления версиями

⚠️ Проблема 2: Cabal hell
   Конфликты зависимостей
   
   Решение:
   Используйте stack вместо cabal
   Или используйте new-style cabal

⚠️ Проблема 3: Compilation time
   Долгая компиляция
   
   Решение:
   Используйте stack build --fast для разработки
   Используйте GHCi для быстрой итерации

⚠️ Проблема 4: Memory usage
   Высокое использование памяти при компиляции
   
   Решение:
   -j1 для single core компиляции
   Увеличить RAM если возможно

⚠️ Проблема 5: Learning curve
   Крутая кривая обучения
   
   Решение:
   Начните с Learn You a Haskell
   Используйте GHCi для экспериментов

⚠️ Проблема 6: Space leaks
   Lazy evaluation может вызвать space leaks
   
   Решение:
   Используйте strictness когда нужно
   Profile для detection

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias ghc='ghc'" >> ~/.bashrc
echo "alias ghc='ghc'" >> ~/.zshrc

echo "alias ghci='ghci'" >> ~/.bashrc
echo "alias ghci='ghci'" >> ~/.zshrc

echo "alias stack='stack'" >> ~/.bashrc
echo "alias stack='stack'" >> ~/.zshrc

echo "alias cabal='cabal'" >> ~/.bashrc
echo "alias cabal='cabal'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия GHC
ghc --version

# Тест 2: Версия Cabal
cabal --version

# Тест 3: Простое вычисление
echo "main = print (2 + 2)" | runghc -

# Тест 4: GHCi
echo ":quit" | ghci

# Тест 5: Stack
stack new test_project simple
cd test_project
stack build
stack run
cd ..
rm -rf test_project

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ БИБЛИОТЕКИ
================================================================================

# Базовые пакеты (cabal/stack):

# Data processing
text
bytestring
vector
containers

# JSON
aeson

# Lenses
lens

# Concurrency
async
stm

# Testing
QuickCheck
hspec
tasty

# Parsing
parsec
megaparsec
attoparsec

# Web
warp
servant
aeson

# Utilities
mtl
transformers
base-compat

================================================================================
                         КОНЕЦ README_HASKELL
================================================================================
