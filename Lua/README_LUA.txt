================================================================================
                    LUA - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Встраиваемый язык + 30+ лет эволюции
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка Lua
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами (LuaRocks)
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые библиотеки

================================================================================
1. УСТАНОВКА LUA
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    LUA = ВСТРАИВАЕМЫЙ ЯЗЫК + 30+ ЛЕТ                         │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  Lua используется:                                                           │
│  • Игры (World of Warcraft, Roblox, Angry Birds)                            │
│  • Встраиваемые системы (embedded)                                          │
│  • Скрипты и автоматизация                                                  │
│  • Nginx (OpenResty)                                                        │
│  • Redis (скрипты)                                                          │
│                                                                              │
│  • Самый лёгкий язык (~300 KB)                                              │
│  • Очень быстрый (C реализация)                                             │
│  • Легко встраивается в C/C++                                               │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Вариант 1: Через apt
sudo apt update
sudo apt install lua5.4 liblua5.4-dev lua5.4-doc

# Вариант 2: Через luarocks (рекомендуется!)
wget https://luarocks.org/releases/luarocks-3.9.2.tar.gz
tar zxpf luarocks-3.9.2.tar.gz
cd luarocks-3.9.2
./configure
make
sudo make install

# Проверка
lua -v
luarocks --version

macOS (Homebrew):
-----------------
brew install lua luarocks

# Проверка
lua -v

Windows:
--------
# Скачать с https://www.lua.org/download.html
# Или использовать Lua for Windows
# Добавить в PATH

# Проверка в PowerShell:
lua -v

Docker (универсально):
----------------------
docker run -it --rm lua:5.4 lua -v

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для Lua                                             │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ VS Code         │ ★★★★★ - С Lua extension (от sumneko)                      │
│ ZeroBrane Studio│ ★★★★★ - Специализированная Lua IDE                        │
│ Vim/Neovim      │ ★★★★☆ - С lua.vim                                         │
│ Emacs           │ ★★★★☆ - С lua-mode                                          │
│ Sublime Text    │ ★★★☆☆ - С Lua package                                     │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка VS Code + Lua:
------------------------
1. Extensions (Ctrl+Shift+X)
2. Установить: "Lua" от sumneko (официальный)
3. Настроить для Lua 5.4

Установка ZeroBrane Studio:
---------------------------
# Скачать с https://studio.zerobrane.com/
# Специализированная IDE для Lua
# Отладчик, автодополнение, и т.д.

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# Lua REPL
lua

# В REPL:
> print("Hello, Lua!")
> 2 + 2
> os.exit()  # Выход

# Запуск скрипта
lua script.lua

# Создание проекта
mkdir my_project && cd my_project

# Структура проекта:
my_project/
├── main.lua         # Главный файл
├── modules/         # Модули
│   └── utils.lua
├── tests/           # Тесты
└── config.lua       # Конфигурация

# Компиляция в байт-код
luac -o main.luac main.lua

# Запуск байт-кода
lua main.luac

# Проверка синтаксиса
luac -p script.lua

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ (LUAROCKS)
================================================================================

# LuaRocks = пакетный менеджер Lua

# Поиск пакетов
luarocks search package_name

# Установка пакета
luarocks install package_name

# Установка конкретной версии
luarocks install package_name 1.0.0

# Удаление пакета
luarocks remove package_name

# Список установленных
luarocks list

# Локальная установка (без sudo)
luarocks install --local package_name

# rockspec файл (аналог package.json):
package = "my_project"
version = "1.0.0-1"
description = {
    summary = "My project",
    homepage = "https://..."
}
dependencies = {
    "lua >= 5.4",
    "luasocket >= 3.0"
}

# Опубликовать пакет
luarocks upload my_project-1.0.0-1.rockspec

# Сообщество пакеты:
# https://luarocks.org/

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: Несколько версий Lua
   lua5.3, lua5.4 могут конфликтовать
   
   Решение: luarocks manage версии
   luarocks config lua_version 5.4

⚠️ Проблема 2: Пакеты не находятся
   module 'foo' not found
   
   Решение:
   Проверить LUA_PATH и LUA_CPATH
   export LUA_PATH="/home/user/.luarocks/share/lua/5.4/?.lua;;"

⚠️ Проблема 3: C библиотеки не компилируются
   Некоторые пакеты требуют C компиляции
   
   Решение:
   sudo apt install build-essential liblua5.4-dev

⚠️ Проблема 4: Path проблемы
   require не находит модули
   
   Решение:
   print(package.path)  # Проверить пути
   Добавить пути в LUA_PATH

⚠️ Проблема 5: Lua 5.1 vs 5.4
   Некоторые пакеты требуют старую версию
   
   Решение:
   luarocks install --lua-version=5.1 package_name

⚠️ Проблема 6: Windows encoding
   Кириллица не отображается
   
   Решение:
   Использовать UTF-8 encoding
   os.setlocale("ru_RU.UTF-8")

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias lua='lua5.4'" >> ~/.bashrc
echo "alias lua='lua5.4'" >> ~/.zshrc

echo "alias lr='luarocks'" >> ~/.bashrc
echo "alias lr='luarocks'" >> ~/.zshrc

echo "alias luac='luac5.4'" >> ~/.bashrc
echo "alias luac='luac5.4'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия Lua
lua -v

# Тест 2: Версия LuaRocks
luarocks --version

# Тест 3: Простое вычисление
echo "print(2 + 2)" | lua

# Тест 4: Установка пакета
luarocks install luasocket
lua -e "local socket = require('socket'); print('OK')"

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ БИБЛИОТЕКИ
================================================================================

# Базовые пакеты (luarocks install):

# Сеть
luarocks install luasocket
luarocks install luafilesystem

# JSON
luarocks install lua-cjson

# Дата и время
luarocks install luadate

# Тестирование
luarocks install busted

# Линтинг
luarocks install luacheck

# Документация
luarocks install ldoc

# Утилиты
luarocks install penlight  # Penlight библиотеки
luarocks install luaunit   # Unit тесты

# Web
luarocks install lapis     # Web фреймворк
luarocks install luvit     # Node.js для Lua

================================================================================
                         КОНЕЦ README_LUA
================================================================================
