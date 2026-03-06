================================================================================
                    F# - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Functional-First + .NET + Production Ready
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка F# (.NET SDK)
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами (NuGet)
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые библиотеки

================================================================================
1. УСТАНОВКА F# (.NET SDK)
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    F# = ML СЕМЬЯ + .NET + PRODUCTION                         │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  F# используется:                                                            │
│  • Финансы и трейдинг                                                       │
│  • Data Science                                                             │
│  • Веб-разработка (ASP.NET)                                                 │
│  • Кроссплатформенные приложения                                            │
│  • Функциональное программирование                                          │
│                                                                              │
│  • Functional-first язык                                                    │
│  • Работает на .NET (CLR)                                                   │
│  • Отличная C# интероперабельность                                          │
│  • 15+ лет развития (2005-2024)                                             │
│  • Production использование                                                 │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Вариант 1: Через .NET SDK (рекомендуется!)
wget https://packages.microsoft.com/config/ubuntu/22.04/packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
sudo apt update
sudo apt install dotnet-sdk-8.0

# Вариант 2: Через snap
sudo snap install dotnet-sdk --classic

# Проверка
dotnet --version
dotnet fsi --version

macOS (Homebrew):
-----------------
brew install --cask dotnet-sdk

# Проверка
dotnet --version

Windows:
--------
# Скачать с https://dotnet.microsoft.com/download
# Установщик .exe включает .NET SDK
# Проверка в PowerShell:
dotnet --version

Docker (универсально):
----------------------
docker run -it --rm mcr.microsoft.com/dotnet/sdk:8.0 dotnet --version

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для F#                                              │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ Visual Studio   │ ★★★★★ - Лучшая поддержка (Windows/macOS)                  │
│ VS Code         │ ★★★★★ - С Ionide extension (кроссплатформенный)           │
│ Rider           │ ★★★★★ - JetBrains IDE (платная)                           │
│ Vim/Neovim      │ ★★★★☆ - С ionide-vim                                      │
│ Emacs           │ ★★★★☆ - С fsharp-mode                                       │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка VS Code + Ionide:
---------------------------
1. Extensions (Ctrl+Shift+X)
2. Установить: "Ionide-fsharp" от Ionide
3. Установить: "Ionide-fake" для build скриптов
4. Установить: "Ionide-paket" для пакетов

Установка Visual Studio:
------------------------
# Windows/macOS
# Скачать с https://visualstudio.microsoft.com/
# Выбрать workload ".NET desktop development"

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# F# Interactive (REPL)
dotnet fsi

# В REPL:
> 2 + 2;;
val it : int = 4
> exit;;  # Выход

# Создание проекта
dotnet new console -lang F# -o my_project
cd my_project

# Структура проекта:
my_project/
├── my_project.fsproj  # Проект файл
├── Program.fs         # Главный файл
└── obj/               # Скомпилированные файлы

# Запуск проекта
dotnet run

# Сборка
dotnet build

# Публикация
dotnet publish

# F# скрипты
dotnet fsi script.fsx

# Компиляция в DLL
dotnet build

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ (NUGET)
================================================================================

# F# использует NuGet (как C#)

# Добавить пакет в проект
dotnet add package PackageName

# Удалить пакет
dotnet remove package PackageName

# Обновить пакеты
dotnet restore

# Поиск пакетов
# https://www.nuget.org/

# Проект файл (.fsproj):
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net8.0</TargetFramework>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="13.0.0" />
  </ItemGroup>
</Project>

# Paket (альтернатива NuGet для F#)
dotnet tool install --global paket
paket init
paket add Newtonsoft.Json
paket install

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: .NET SDK не найден
   dotnet: command not found
   
   Решение:
   Установить .NET SDK 8.0+
   Проверить PATH

⚠️ Проблема 2: Ionide не работает в VS Code
   Автодополнение не работает
   
   Решение:
   Установить .NET SDK
   Перезапустить VS Code
   Проверить Output → Ionide

⚠️ Проблема 3: Конфликт версий .NET
   Разные проекты требуют разные версии
   
   Решение:
   Использовать global.json
   dotnet new globaljson --sdk-version 8.0.0

⚠️ Проблема 4: F# Interactive медленный
   Первый запуск долгий
   
   Решение:
   Это нормально - загрузка .NET runtime
   Последующие запуски быстрее

⚠️ Проблема 5: Неправильный порядок файлов
   F# компилирует файлы по порядку
   
   Решение:
   Указать порядок в .fsproj файле
   <Compile Include="Module1.fs" />
   <Compile Include="Module2.fs" />

⚠️ Проблема 6: C# интероперабельность
   Сложности с C# библиотеками
   
   Решение:
   Использовать F# friendly API
   Изучить F# C# interop guide

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias fs='dotnet fsi'" >> ~/.bashrc
echo "alias fs='dotnet fsi'" >> ~/.zshrc

echo "alias fsr='dotnet run'" >> ~/.bashrc
echo "alias fsr='dotnet run'" >> ~/.zshrc

echo "alias fsb='dotnet build'" >> ~/.bashrc
echo "alias fsb='dotnet build'" >> ~/.zshrc

echo "alias fst='dotnet test'" >> ~/.bashrc
echo "alias fst='dotnet test'" >> ~/.zshrc

echo "alias fsp='dotnet publish'" >> ~/.bashrc
echo "alias fsp='dotnet publish'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия .NET
dotnet --version

# Тест 2: F# Interactive
echo "2 + 2;;" | dotnet fsi

# Тест 3: Создание проекта
dotnet new console -lang F# -o test_project
cd test_project
dotnet run
cd ..
rm -rf test_project

# Тест 4: Скрипт
echo 'printfn "OK"' > test.fsx
dotnet fsi test.fsx
rm test.fsx

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ БИБЛИОТЕКИ
================================================================================

# Базовые пакеты (dotnet add package):

# JSON
dotnet add package Newtonsoft.Json
dotnet add package System.Text.Json

# Веб
dotnet add package Giraffe
dotnet add package Saturn

# Data Science
dotnet add package Deedle
dotnet add package FSharp.Data

# Тестирование
dotnet add package Expecto
dotnet add package FsUnit

# Утилиты
dotnet add package FSharp.Core
dotnet add package FsCheck

# Асинхронность
# Встроено в F# (Async, Task)

# Базы данных
dotnet add package FSharp.Data.SqlClient
dotnet add package Dapper

================================================================================
                         КОНЕЦ README_FSHARP
================================================================================
