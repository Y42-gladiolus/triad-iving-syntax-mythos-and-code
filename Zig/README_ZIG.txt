================================================================================
                    ZIG - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Системное программирование + C совместимость
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка Zig
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые библиотеки

================================================================================
1. УСТАНОВКА ZIG
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    ZIG = СОВРЕМЕННЫЙ C БЕЗ GC                                │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  Zig компилируется в native код:                                             │
│  • Нет runtime (кроме стандартной библиотеки)                               │
│  • Прямая интероперабельность с C                                           │
│  • Compile-time code execution (comptime)                                   │
│  • Manual memory management (как C, но безопаснее)                          │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Вариант 1: Официальный скрипт установки
curl -L https://ziglang.org/download/0.11.0/zig-linux-x86_64-0.11.0.tar.xz | tar -xJ
sudo mv zig-linux-x86_64-0.11.0 /opt/zig
sudo ln -s /opt/zig/zig /usr/local/bin/zig

# Вариант 2: Через asdf
asdf plugin-add zig
asdf install zig latest
asdf global zig latest

# Вариант 3: Через snap
sudo snap install zig --classic --beta

# Проверка
zig version

macOS (Homebrew):
-----------------
brew install zig

# Проверка
zig version

Windows:
--------
# Скачать с https://ziglang.org/download/
# Распаковать архив
# Добавить в PATH: C:\zig\zig.exe

# Проверка в PowerShell:
zig version

Docker (универсально):
----------------------
docker run -it --rm zigimg/zig zig version

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для Zig                                             │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ VS Code         │ ★★★★★ - С Zig extension (официальный)                     │
│ Vim/Neovim      │ ★★★★☆ - С zig.vim + zls                                   │
│ Emacs           │ ★★★★☆ - С zig-mode + zls                                  │
│ Helix           │ ★★★★☆ - Встроенная поддержка Zig                          │
│ Zed             │ ★★★★☆ - Встроенная поддержка                              │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка VS Code + Zig:
------------------------
1. Extensions (Ctrl+Shift+X)
2. Установить: "Zig" от Zig Language Server
3. Установить: "ZLS" для автодополнения

Установка ZLS (Zig Language Server):
------------------------------------
git clone https://github.com/zigtools/zls.git
cd zls
zig build -Drelease-safe
sudo cp zig-out/bin/zls /usr/local/bin/

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# Создание проекта
zig init-exe my_project
cd my_project

# Структура проекта:
my_project/
├── build.zig        # Build скрипт
├── src/
│   └── main.zig     # Исходный код
└── zig-out/         # Скомпилированные файлы

# Запуск проекта
zig build run

# Компиляция
zig build

# Компиляция в release mode
zig build -Doptimize=ReleaseFast

# Запуск без сборки (скрипт)
zig run src/main.zig

# Форматирование
zig fmt src/main.zig

# Тесты
zig build test

# Cross-компиляция (встроенная!)
zig build -Dtarget=x86_64-windows
zig build -Dtarget=aarch64-macos

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ
================================================================================

# Zig имеет встроенный пакетный менеджер

# Добавить зависимость (в build.zig):
const deps = b.addModule("deps", .{
    .root_source_file = .{ .path = "deps/src/root.zig" },
});

# Или через zig fetch:
zig fetch --save https://github.com/user/repo/archive/commit.tar.gz

# Структура zig.zon:
.{
    .name = "my_project",
    .version = "0.1.0",
    .dependencies = .{
        .{
            .name = "dependency",
            .url = "https://...",
            .hash = "1234567890...",
        },
    },
}

# Обновить зависимости
zig fetch --save-url https://...

# Сообщество пакеты:
# https://github.com/ziglibs/zig-libraries
# https://github.com/HeapsUp/zig-packages

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: zig не в PATH
   zig: command not found
   
   Решение:
   export PATH="/opt/zig:$PATH"
   Добавить в ~/.bashrc

⚠️ Проблема 2: Конфликт версий
   Разные проекты требуют разные версии
   
   Решение: asdf manage версии
   asdf local zig 0.11.0

⚠️ Проблема 3: ZLS не работает
   Автодополнение не работает
   
   Решение:
   Скомпилировать ZLS из исходников
   Проверить что zls в PATH

⚠️ Проблема 4: Cross-компиляция не работает
   Требуются sysroot файлы
   
   Решение:
   Zig включает sysroot для многих targets
   zig build -Dtarget=x86_64-linux-gnu

⚠️ Проблема 5: C интероперабельность
   Не находит C заголовки
   
   Решение:
  zig build -lc  # Линковать с libc

⚠️ Проблема 6: Debug vs Release
   Debug сборка медленная
   
   Решение:
   zig build -Doptimize=ReleaseFast для production

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias z='zig'" >> ~/.bashrc
echo "alias z='zig'" >> ~/.zshrc

echo "alias zb='zig build'" >> ~/.bashrc
echo "alias zb='zig build'" >> ~/.zshrc

echo "alias zr='zig build run'" >> ~/.bashrc
echo "alias zr='zig build run'" >> ~/.zshrc

echo "alias zt='zig build test'" >> ~/.bashrc
echo "alias zt='zig build test'" >> ~/.zshrc

echo "alias zf='zig fmt'" >> ~/.bashrc
echo "alias zf='zig fmt'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия Zig
zig version

# Тест 2: Простое вычисление
echo 'const std = @import("std"); pub fn main() !void { std.debug.print("{}\n", .{2 + 2}); }' | zig run -

# Тест 3: Создание и запуск проекта
zig init-exe test_project
cd test_project
zig build run
cd ..
rm -rf test_project

# Тест 4: Форматирование
echo 'fn main()void{}' | zig fmt -

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ БИБЛИОТЕКИ
================================================================================

# Базовые библиотеки (добавить через zig fetch):

# HTTP клиент
https://github.com/karlseguin/http.zig

# JSON парсинг
# Встроено в std.json

# Тестирование
# Встроено в zig test

# Асинхронность
https://github.com/ziglibs/zig-async

# Строки
https://github.com/ziglibs/zig-string

# Математика
https://github.com/ziglibs/zig-math

# C интероперабельность
# Встроено (@cImport, @cInclude)

================================================================================
                         КОНЕЦ README_ZIG
================================================================================
