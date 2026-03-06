================================================================================
                    DART - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Кроссплатформенный UI + Flutter
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка Dart (SDK)
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами (Pub)
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые пакеты

================================================================================
1. УСТАНОВКА DART (SDK)
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    DART = ЯЗЫК ДЛЯ FLUTTER + WEB + SERVER                    │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  Dart компилируется в:                                                       │
│  • Native code (AOT) — для mobile/desktop                                   │
│  • JavaScript — для web                                                     │
│  • JIT — для разработки (hot reload)                                        │
│                                                                              │
│  Flutter = UI фреймворк на Dart                                             │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Вариант 1: Через apt (официальный репозиторий)
sudo apt update
sudo apt install apt-transport-https
wget -qO- https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo gpg --dearmor -o /usr/share/keyrings/dart.gpg
echo 'deb [signed-by=/usr/share/keyrings/dart.gpg arch=amd64] https://storage.googleapis.com/download.dartlang.org/linux/debian stable main' | sudo tee /etc/apt/sources.list.d/dart_stable.list
sudo apt update
sudo apt install dart

# Вариант 2: Через snap
sudo snap install dart --classic

# Вариант 3: Через asdf
asdf plugin-add dart
asdf install dart latest
asdf global dart latest

# Добавить в PATH
export PATH="$PATH:$HOME/.pub-cache/bin"
echo 'export PATH="$PATH:$HOME/.pub-cache/bin"' >> ~/.bashrc

# Проверка
dart --version

macOS (Homebrew):
-----------------
brew tap dart-lang/dart
brew install dart

# Проверка
dart --version

Windows:
--------
# Скачать с https://dart.dev/get-dart
# Установщик .exe
# Добавить в PATH: C:\Program Files\Dart\bin

# Проверка в PowerShell:
dart --version

Docker (универсально):
----------------------
docker run -it --rm google/dart dart --version

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для Dart                                            │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ IntelliJ IDEA   │ ★★★★★ - Лучшая поддержка Dart/Flutter                     │
│ VS Code         │ ★★★★★ - С Dart extension (официальный)                    │
│ Android Studio  │ ★★★★★ - Для Flutter mobile development                    │
│ Vim/Neovim      │ ★★★☆☆ - С dart-vim-plugin                                 │
│ Emacs           │ ★★★☆☆ - С dart-mode                                       │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка VS Code + Dart:
-------------------------
1. Extensions (Ctrl+Shift+X)
2. Установить: "Dart" от Dart Code
3. Установить: "Flutter" (если нужен Flutter)

Установка IntelliJ IDEA:
------------------------
1. Скачать с https://www.jetbrains.com/idea/
2. Установить Dart plugin
3. Установить Flutter plugin (если нужен)

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# Создание проекта
dart create my_project
cd my_project

# Структура проекта:
my_project/
├── pubspec.yaml       # Конфигурация проекта
├── bin/               # Исполняемые файлы
│   └── my_project.dart
├── lib/               # Библиотеки
│   └── my_project.dart
├── test/              # Тесты
│   └── my_project_test.dart
└── .dart_tool/        # Инструменты

# Запуск проекта
dart run

# Запуск с аргументами
dart run bin/my_project.dart arg1 arg2

# Форматирование
dart format .

# Анализ кода
dart analyze

# Тесты
dart test

# Создание Flutter приложения
flutter create my_app
cd my_app
flutter run

# Компиляция в native (AOT)
dart compile exe bin/my_project.dart
./bin/my_project.exe

# Компиляция в JavaScript
dart compile js bin/my_project.dart -o web/my_project.js

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ (PUB)
================================================================================

# Pub = пакетный менеджер Dart

# Добавить зависимость (в pubspec.yaml):
dependencies:
  http: ^1.1.0
  json_annotation: ^4.8.0
  provider: ^6.1.0  # Для Flutter

# Установить зависимости
dart pub get

# Обновить зависимости
dart pub upgrade

# Добавить пакет через CLI
dart pub add http
dart pub add --dev test

# Опубликовать пакет
dart pub publish

# Поиск пакетов
# https://pub.dev/packages

# Глобальные пакеты
dart pub global activate <package>
dart pub global run <package>

# Примеры глобальных пакетов:
dart pub global activate webdev      # Web development
dart pub global activate build_runner  # Code generation

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: PATH не настроен
   dart: command not found
   
   Решение:
   export PATH="$PATH:$HOME/.pub-cache/bin"
   Добавить в ~/.bashrc

⚠️ Проблема 2: Конфликт версий
   Разные проекты требуют разные версии
   
   Решение: asdf manage версии
   asdf local dart 3.2.0  # Для конкретного проекта

⚠️ Проблема 3: Flutter не установлен (для mobile)
   Flutter требует отдельной установки
   
   Решение:
   git clone https://github.com/flutter/flutter.git
   export PATH="$PATH:$HOME/flutter/bin"

⚠️ Проблема 4: Android SDK не настроен (для Android)
   Flutter не может компилировать для Android
   
   Решение:
   flutter doctor --android-licenses
   flutter config --android-sdk /path/to/sdk

⚠️ Проблема 5: Xcode не установлен (для iOS на macOS)
   Flutter не может компилировать для iOS
   
   Решение:
   sudo xcode-select --install
   sudo xcodebuild -runFirstLaunch

⚠️ Проблема 6: Pub cache проблемы
   Pub не может скачать пакеты
   
   Решение:
   rm -rf ~/.pub-cache
   dart pub get

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias d='dart'" >> ~/.bashrc
echo "alias d='dart'" >> ~/.zshrc

echo "alias dr='dart run'" >> ~/.bashrc
echo "alias dr='dart run'" >> ~/.zshrc

echo "alias dt='dart test'" >> ~/.bashrc
echo "alias dt='dart test'" >> ~/.zshrc

echo "alias df='dart format'" >> ~/.bashrc
echo "alias df='dart format'" >> ~/.zshrc

echo "alias da='dart analyze'" >> ~/.bashrc
echo "alias da='dart analyze'" >> ~/.zshrc

echo "alias dp='dart pub'" >> ~/.bashrc
echo "alias dp='dart pub'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия Dart
dart --version

# Тест 2: Простое вычисление
echo "main() => print(2 + 2);" | dart run -

# Тест 3: Создание и запуск проекта
dart create test_project
cd test_project
dart run
cd ..
rm -rf test_project

# Тест 4: Форматирование
echo "main()=>print(1);" | dart format -

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ ПАКЕТЫ
================================================================================

# Базовые пакеты (добавить в pubspec.yaml):
dependencies:
  # HTTP клиент
  http: ^1.1.0
  
  # JSON сериализация
  json_annotation: ^4.8.0
  json_serializable: ^6.7.0
  
  # State management (Flutter)
  provider: ^6.1.0
  riverpod: ^2.4.0
  
  # Утилиты
  collection: ^1.18.0
  meta: ^1.10.0
  equatable: ^2.0.5
  
  # Асинхронность
  async: ^2.11.0
  rxdart: ^0.27.0
  
  # CLI утилиты
  args: ^2.4.0
  cli_util: ^0.4.0

# Для разработки:
dev_dependencies:
  test: ^1.24.0
  build_runner: ^2.4.0
  lints: ^3.0.0

================================================================================
                         КОНЕЦ README_DART
================================================================================
