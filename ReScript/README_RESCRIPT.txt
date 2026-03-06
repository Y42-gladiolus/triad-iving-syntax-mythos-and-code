================================================================================
                    RE SCRIPT - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Типы которые работают + JS экосистема
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка ReScript
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые пакеты

================================================================================
1. УСТАНОВКА RE SCRIPT
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    RE SCRIPT = OCAML ДЛЯ JAVASCRIPT                          │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  ReScript используется:                                                      │
│  • Веб-разработка (компилируется в JS)                                      │
│  • React приложения (ReScript React)                                        │
│  • Когда TypeScript типы недостаточно надёжны                               │
│  • Full-stack разработка                                                    │
│  • Node.js backend                                                          │
│                                                                              │
│  • Компилируется в чистый, читаемый JS                                     │
│  • Быстрая компиляция                                                       │
│  • 100% интероперабельность с JS                                            │
│  • Строгая типизация (без any!)                                             │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux/macOS/Windows:
--------------------
# Требуется Node.js (14+)
# Проверить: node --version

# Установка ReScript
npm install -g rescript

# Или локально в проект
npm install --save-dev rescript

# Проверка
rescript --version

# Инициализация проекта
rescript init

# Или с React шаблоном
npx create-rescript-app my-app

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для ReScript                                        │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ VS Code         │ ★★★★★ - С ReScript extension (официальный)                │
│ Vim/Neovim      │ ★★★★☆ - С rescript-vim                                    │
│ Emacs           │ ★★★★☆ - С rescript-mode                                     │
│ WebStorm        │ ★★★☆☆ - С плагином                                        │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка VS Code + ReScript:
-----------------------------
1. Extensions (Ctrl+Shift+X)
2. Установить: "ReScript" от ReScript
3. Установить: "ReScript Platform" для лучшей поддержки

Настройка:
----------
# В settings.json:
{
  "rescript.editor.settings": {
    "allowBuiltInComponentLinting": true
  }
}

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# Создание проекта
rescript init my_project
cd my_project

# Структура проекта:
my_project/
├── rescript.json        # Конфигурация
├── package.json         # Node.js зависимости
├── src/                 # Исходный код
│   └── Index.res
├── bsconfig.json        # ReScript конфиг (старый формат)
└── lib/                 # Скомпилированный JS

# Запуск компилятора
rescript build

# Запуск в watch режиме
rescript build -w

# Запуск проекта
node lib/Index.js

# С React:
npx create-rescript-app my-app
cd my-app
rescript build -w

# Компиляция в разные форматы
# ES6 modules, CommonJS, etc. (в rescript.json)

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ
================================================================================

# ReScript использует npm для пакетов

# Установка ReScript пакетов
npm install @rescript/react
npm install @rescript/core

# Установка JS пакетов (с bindings)
npm install lodash
# Создать bindings вручную или использовать genType

# ReScript пакеты:
# https://rescript-lang.org/packages

# rescript.json зависимости:
{
  "name": "my-project",
  "version": "1.0.0",
  "dependencies": {
    "@rescript/react": "*",
    "@rescript/core": "*"
  },
  "bs-dependencies": [
    "@rescript/react",
    "@rescript/core"
  ]
}

# Генерация bindings для JS библиотек
# https://github.com/rescript-community/rescript-bindgen

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: Node.js версия
   ReScript требует Node.js 14+
   
   Решение:
   nvm install 18
   nvm use 18

⚠️ Проблема 2: Конфликт bsconfig.json и rescript.json
   Старые проекты используют bsconfig.json
   
   Решение:
   Использовать rescript.json (новый формат)
   Или обновить проект: rescript upgrade

⚠️ Проблема 3: Bindings для JS библиотек
   Нет готовых bindings для некоторых пакетов
   
   Решение:
   Создать bindings вручную
   Или использовать genType для авто-генерации

⚠️ Проблема 4: VS Code extension не работает
   Автодополнение не работает
   
   Решение:
   rescript build -w  # Запустить компилятор в watch режиме
   Перезапустить VS Code

⚠️ Проблема 5: TypeScript интероперабельность
   Сложности с TS типами
   
   Решение:
   Использовать @genType decorators
   Или создать .d.ts файлы вручную

⚠️ Проблема 6: Старый ReasonML синтаксис
   Некоторые примеры используют старый синтаксис
   
   Решение:
   Использовать ReScript синтаксис (новый)
   https://rescript-lang.org/docs/manual/latest/introduction

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias rs='rescript'" >> ~/.bashrc
echo "alias rs='rescript'" >> ~/.zshrc

echo "alias rsb='rescript build'" >> ~/.bashrc
echo "alias rsb='rescript build'" >> ~/.zshrc

echo "alias rsw='rescript build -w'" >> ~/.bashrc
echo "alias rsw='rescript build -w'" >> ~/.zshrc

echo "alias rsi='rescript init'" >> ~/.bashrc
echo "alias rsi='rescript init'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия ReScript
rescript --version

# Тест 2: Инициализация проекта
rescript init test_project
cd test_project
rescript build
cd ..
rm -rf test_project

# Тест 3: Простая компиляция
echo 'let x = 2 + 2' > Test.res
rescript build
rm Test.res lib/Test.js

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ ПАКЕТЫ
================================================================================

# Базовые пакеты (npm install):

# React
npm install @rescript/react

# Утилиты
npm install @rescript/core

# HTTP клиент
npm install axios
# Создать bindings

# Роутинг
npm install @rescript/react-router

# Тестирование
npm install --save-dev @glennsl/rescript-jest

# Форматирование
# Встроено: rescript format

# Linting
npm install --save-dev @rescript/bslint

# GenType для TS интероперабельности
npm install --save-dev gentype

================================================================================
                         КОНЕЦ README_RESCRIPT
================================================================================
