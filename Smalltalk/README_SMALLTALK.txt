================================================================================
                    SMALLTALK - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Pure OOP + Live Coding + Image-based + 50+ лет
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка Smalltalk (Pharo/Squeak)
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые библиотеки

================================================================================
1. УСТАНОВКА SMALLTALK
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    SMALLTALK = PURE OOP + LIVE ENVIRONMENT                   │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  Smalltalk используется:                                                     │
│  • Education (обучение ООП)                                                 │
│  • Rapid prototyping                                                        │
│  • Live coding environment                                                  │
│  • Image-based development                                                  │
│  • Influence на Objective-C, Java, Ruby, Python                             │
│                                                                              │
│  • 50+ лет развития (1972-2024)                                             │
│  • Всё — объект (даже числа, классы)                                        │
│  • Image-based (сохраняете состояние)                                       │
│  • Live coding (изменяете код на лету)                                      │
│  • Pure OOP (нет примитивов)                                                │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Pharo (современная реализация)
wget -O- get.pharo.org/64+vm | bash

# Или Squeak
sudo apt install squeak-vm

# Проверка
./pharo Pharo.image

macOS (Homebrew):
-----------------
brew install --cask pharo

# Или Squeak
brew install --cask squeak

# Проверка
open Pharo.app

Windows:
--------
# Pharo
# Скачать с https://pharo.org/download

# Squeak
# Скачать с https://squeak.org/download/

# Запустить .exe файл

Docker (универсально):
----------------------
docker run -it --rm pharo/project-run pharo

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для Smalltalk                                       │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ Pharo IDE       │ ★★★★★ - Встроенная IDE (лучшая поддержка)                 │
│ Squeak IDE      │ ★★★★★ - Встроенная IDE                                     │
│ VisualWorks     │ ★★★★★ - Коммерческая IDE                                   │
│ VS Code         │ ★★☆☆☆ - С Smalltalk extension (ограниченная)              │
│ Vim/Neovim      │ ★★☆☆☆ - С smalltalk.vim                                    │
└─────────────────┴────────────────────────────────────────────────────────────┘

Pharo IDE (встроена):
---------------------
# Запускается вместе с Pharo
# Включает:
# - Browser (код)
# - Workspace (код)
# - Transcript (вывод)
# - Inspector (объекты)
# - Debugger (отладка)

Squeak IDE (встроена):
----------------------
# Запускается вместе с Squeak
# Аналогичный функционал

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# Запуск Pharo
./pharo Pharo.image

# В Workspace:
'Hello, Smalltalk!' displayNl.

# Простые вычисления
5 + 3.
5 * 3.
5 squared.

# Создание класса
Object subclass: #Person
    instanceVariableNames: 'name age'
    classVariableNames: ''
    package: 'MyPackage'

# Создание экземпляра
p := Person new.
p name: 'John'.
p age: 25.

# Методы
Person >> greet
    ^ 'Hello, ', self name

# Запуск метода
p greet.

# Сохранение image
Smalltalk saveSession.

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ
================================================================================

# Pharo использует Metacello
Metacello new
    baseline: 'MyProject';
    repository: 'github://user/project:master/src';
    load.

# Популярные пакеты:
# - NeoJSON (JSON parsing)
# - Zinc HTTP Components (web server)
# - Roassal (visualization)
# - Moose (software analysis)

# Установка через Catalog Browser
# В Pharo: Tools → Catalog Browser

# BaselineOfMyProject.class.st
BaselineOf subclass: #BaselineOfMyProject
    instanceVariableNames: ''
    classVariableNames: ''
    package: 'BaselineOfMyProject'

BaselineOfMyProject >> baseline: spec
    <baseline>
    spec for: #common do: [
        spec package: 'MyProject'
    ]

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: Image-based development
   Нет традиционных файлов с кодом
   
   Решение:
   Использовать Metacello для экспорта
   Или работать внутри image

⚠️ Проблема 2: Нет command line (традиционно)
   Smalltalk обычно GUI
   
   Решение:
   Использовать Pharo headless mode
   ./pharo Pharo.image eval "5 + 3"

⚠️ Проблема 3: Версии Smalltalk
   Pharo vs Squeak vs VisualWorks
   
   Решение:
   Использовать Pharo для современных проектов
   Squeak для education

⚠️ Проблема 4: Память image
   Image может расти со временем
   
   Решение:
   Регулярно сохранять clean image
   Использовать garbage collection

⚠️ Проблема 5: Интеграция с внешним миром
   FFI может быть сложным
   
   Решение:
   Использовать FFI library
   Или использовать REST API

⚠️ Проблема 6: Сообщество меньше
   Меньше чем у mainstream языков
   
   Решение:
   Присоединиться к Pharo mailing list
   Читать Pharo books

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias pharo='./pharo Pharo.image'" >> ~/.bashrc
echo "alias pharo='./pharo Pharo.image'" >> ~/.zshrc

echo "alias squeak='squeak Squeak.image'" >> ~/.bashrc
echo "alias squeak='squeak Squeak.image'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Запуск Pharo
./pharo Pharo.image eval "5 + 3"

# Тест 2: Простое вычисление
./pharo Pharo.image eval "'Hello' size"

# Тест 3: Создание класса
./pharo Pharo.image eval "
Object subclass: #TestClass
    instanceVariableNames: ''
    classVariableNames: ''
    package: 'TestPackage'
"

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ БИБЛИОТЕКИ
================================================================================

# Базовые библиотеки (Metacello):

# JSON
Metacello new
    baseline: 'NeoJSON';
    repository: 'github://svenvc/NeoJSON:master/repository';
    load.

# HTTP server
Metacello new
    baseline: 'ZincHTTPComponents';
    repository: 'github://svenvc/ZincHTTPComponents:master/repository';
    load.

# Visualization
Metacello new
    baseline: 'Roassal';
    repository: 'github://ObjectProfile/Roassal3:master/src';
    load.

# Testing
Metacello new
    baseline: 'SUnit';
    repository: 'github://pharo-project/pharo:Pharo-9.0/src';
    load.

# Database
Metacello new
    baseline: 'Pillar';
    repository: 'github://pillar-markup/Pillar:Pharo9.0/src';
    load.

================================================================================
                         КОНЕЦ README_SMALLTALK
================================================================================
