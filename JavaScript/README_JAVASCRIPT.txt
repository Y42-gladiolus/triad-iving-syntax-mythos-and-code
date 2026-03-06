================================================================================
                    JAVASCRIPT - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Язык веба + Node.js + 28 лет эволюции
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка Node.js (npm)
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами (npm/yarn/pnpm)
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые пакеты

================================================================================
1. УСТАНОВКА NODE.JS (NPM)
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    JAVASCRIPT = ЯЗЫК ВЕБА + NODE.JS                          │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  JavaScript работает:                                                        │
│  • В браузере (frontend)                                                    │
│  • На сервере (Node.js, Deno, Bun)                                          │
│  • Везде (IoT, mobile, desktop)                                             │
│                                                                              │
│  • Самая большая экосистема (npm = 3+ млн пакетов)                          │
│  • 28 лет развития (1995-2024)                                              │
│  • ES6+ (современный стандарт)                                              │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Вариант 1: Через nvm (рекомендуется!)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
source ~/.bashrc
nvm install --lts
nvm use --lts

# Вариант 2: Через apt (может быть старая версия)
sudo apt update
sudo apt install nodejs npm

# Проверка
node --version
npm --version

macOS (Homebrew):
-----------------
brew install node

# Проверка
node --version

Windows:
--------
# Скачать с https://nodejs.org/
# Установщик .exe включает npm
# Проверка в PowerShell:
node --version

Docker (универсально):
----------------------
docker run -it --rm node:latest node --version

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для JavaScript                                      │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ VS Code         │ ★★★★★ - Лучшая поддержка (от Microsoft!)                  │
│ WebStorm        │ ★★★★★ - Платная IDE (JetBrains)                           │
│ Vim/Neovim      │ ★★★★☆ - С coc.nvim                                        │
│ Emacs           │ ★★★★☆ - С js2-mode + lsp                                  │
│ Sublime Text    │ ★★★☆☆ - С Babel package                                   │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка VS Code + JavaScript:
-------------------------------
1. VS Code имеет встроенную поддержку JavaScript!
2. Extensions (опционально):
   - "ESLint" для линтинга
   - "Prettier" для форматирования
   - "npm Intellisense" для автодополнения

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# Создание проекта
npm init -y

# Структура проекта:
my_project/
├── package.json       # Зависимости и скрипты
├── src/               # Исходный код
│   └── index.js
├── tests/             # Тесты
└── node_modules/      # Зависимости

# Запуск скрипта
node src/index.js

# Node.js REPL
node

# В REPL:
> 2 + 2
4
> .exit  # Выход

# Modern ES6 модули
# В package.json добавить: "type": "module"
# Или использовать .mjs расширение

# Компиляция (Babel для старых браузеров)
npm install --save-dev @babel/core @babel/cli
npx babel src --out-dir dist

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ (NPM/YARN/PNPM)
================================================================================

# npm (идёт с Node.js)
npm install package_name
npm install package_name --save-dev
npm uninstall package_name
npm update
npm outdated

# yarn (альтернатива npm)
npm install -g yarn
yarn add package_name
yarn add package_name --dev
yarn remove package_name

# pnpm (быстрее, меньше места)
npm install -g pnpm
pnpm add package_name
pnpm add package_name --save-dev

# package.json зависимости:
{
  "dependencies": {
    "express": "^4.18.0",      # Совместимые версии
    "lodash": "~4.17.0"        # Только patch версии
  },
  "devDependencies": {
    "jest": "^29.0.0",         # Только для разработки
    "eslint": "^8.0.0"
  }
}

# Скрипты в package.json:
{
  "scripts": {
    "start": "node src/index.js",
    "test": "jest",
    "lint": "eslint src/",
    "build": "babel src --out-dir dist"
  }
}

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: Глобальные пакеты требуют sudo (Linux)
   npm install -g package → Permission denied
   
   Решение:
   mkdir ~/.npm-global
   npm config set prefix '~/.npm-global'
   export PATH=~/.npm-global/bin:$PATH

⚠️ Проблема 2: Конфликт версий Node.js
   Разные проекты требуют разные версии
   
   Решение: nvm manage версии
   nvm install 18
   nvm use 18
   nvm alias default 18

⚠️ Проблема 3: node_modules занимает много места
   Может занимать GBs
   
   Решение: pnpm использует меньше места

⚠️ Проблема 4: ES6 модули не работают
   import/export не работают
   
   Решение в package.json:
   { "type": "module" }
   Или использовать .mjs расширение

⚠️ Проблема 5: Babel трансформация
   Старые браузеры не поддерживают ES6
   
   Решение:
   npm install --save-dev @babel/core @babel/preset-env

⚠️ Проблема 6: npm audit warnings
   Уязвимости в зависимостях
   
   Решение:
   npm audit fix
   npm audit fix --force

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias js='node'" >> ~/.bashrc
echo "alias js='node'" >> ~/.zshrc

echo "alias ni='npm install'" >> ~/.bashrc
echo "alias ni='npm install'" >> ~/.zshrc

echo "alias ns='npm start'" >> ~/.bashrc
echo "alias ns='npm start'" >> ~/.zshrc

echo "alias nt='npm test'" >> ~/.bashrc
echo "alias nt='npm test'" >> ~/.zshrc

echo "alias nl='npm run lint'" >> ~/.bashrc
echo "alias nl='npm run lint'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия Node.js
node --version

# Тест 2: Версия npm
npm --version

# Тест 3: Простое вычисление
echo "console.log(2 + 2);" | node

# Тест 4: Создание и запуск проекта
npm init -y
echo "console.log('OK');" > index.js
node index.js
rm package.json package-lock.json index.js

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ ПАКЕТЫ
================================================================================

# Базовые пакеты (добавить в package.json):
{
  "dependencies": {
    # Web фреймворки
    "express": "^4.18.0",        # Backend
    "react": "^18.0.0",          # Frontend
    "vue": "^3.0.0",             # Frontend
    
    # Утилиты
    "lodash": "^4.17.0",         # Утилиты
    "axios": "^1.6.0",           # HTTP клиент
    "moment": "^2.29.0",         # Дата и время
    
    # JSON
    "joi": "^17.0.0",            # Валидация схем
  },
  
  "devDependencies": {
    # Тестирование
    "jest": "^29.0.0",           # Тесты
    "mocha": "^10.0.0",          # Тесты
    
    # Линтинг
    "eslint": "^8.0.0",          # Линтер
    "prettier": "^3.0.0",        # Форматирование
    
    # Сборка
    "webpack": "^5.0.0",         # Bundler
    "babel": "^7.0.0"            # Транспиляция
  }
}

================================================================================
                         КОНЕЦ README_JAVASCRIPT
================================================================================
