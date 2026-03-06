================================================================================
                    BASH - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Universal Shell + GNU + 30+ лет эволюции
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка Bash
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые утилиты

================================================================================
1. УСТАНОВКА BASH
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    BASH = UNIVERSAL SHELL + GNU EXTENSIONS                   │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  Bash используется:                                                          │
│  • System scripting                                                         │
│  • Shell scripts                                                            │
│  • Interactive shell                                                        │
│  • DevOps и automation                                                      │
│  • CI/CD pipelines                                                          │
│                                                                              │
│  • GNU Bash (Bourne Again SHell)                                            │
│  • 30+ лет развития (1989-2024)                                             │
│  • Обратная совместимость с sh                                              │
│  • Огромная экосистема                                                      │
│  • Стандарт де-факто для Linux                                              │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Bash обычно предустановлен
bash --version

# Если нет:
sudo apt update
sudo apt install bash

# Проверка
bash --version

macOS:
------
# Bash предустановлен (старая версия)
bash --version

# Новая версия через Homebrew:
brew install bash

# Добавить в /etc/shells
echo "/usr/local/bin/bash" | sudo tee -a /etc/shells

Windows:
--------
# Через WSL (рекомендуется)
# Или через Git Bash
# Или через Cygwin/MSYS2

# Проверка в PowerShell:
bash --version

Docker (универсально):
----------------------
docker run -it --rm ubuntu:latest bash --version
docker run -it --rm alpine:latest bash --version

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для Bash                                            │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ Vim/Neovim      │ ★★★★★ - С sh.vim (отличная поддержка)                     │
│ Emacs           │ ★★★★★ - С sh-mode                                           │
│ VS Code         │ ★★★★★ - С Bash IDE extension                              │
│ Teko            │ ★★★★☆ - Специализированный Bash editor                    │
│ Текстовый + CLI │ ★★★★★ - Классический способ                                │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка Vim + sh.vim:
-----------------------
# Встроен в Vim
(add-to-list 'auto-mode-alist '("\\.sh$" . sh-mode))

Установка VS Code + Bash IDE:
-----------------------------
1. Extensions (Ctrl+Shift+X)
2. Установить: "Bash IDE" от Mads Hartmann
3. Установить: "ShellCheck" от Timon Wong

Установка ShellCheck:
---------------------
sudo apt install shellcheck

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# Bash REPL (интерактивный режим)
bash

# В REPL:
$ echo "Hello"
$ exit  # Выход

# Shebang для скриптов
#!/bin/bash

# Или с env (более portable)
#!/usr/bin/env bash

# Запуск скрипта
bash script.sh

# Или через shebang
chmod +x script.sh
./script.sh

# Создание проекта
mkdir my_project && cd my_project

# Структура проекта:
my_project/
├── script.sh        # Главный скрипт
├── lib/             # Библиотеки функций
│   └── functions.sh
├── config.sh        # Конфигурация
└── README.md        # Документация

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ
================================================================================

# Bash не имеет пакетного менеджера
# Скрипты = .sh файлы

# Поиск скриптов:
# https://github.com/bash
# https://shellcheck.net/
# https://github.com/awesome-bash

# Подключение библиотек
# Через source или .
source ./lib/functions.sh
. ./lib/functions.sh

# Структура библиотеки:
# lib/functions.sh
my_function() {
    echo "Hello from function"
}

# Использование
#!/bin/bash
source ./lib/functions.sh
my_function

# Bash packages (bash-it, oh-my-bash)
# https://github.com/Bash-it/bash-it
# https://github.com/ohmybash/oh-my-bash

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: Версия bash
   macOS имеет старую версию (3.2)
   
   Решение:
   brew install bash
   Изменить shell: chsh -s /usr/local/bin/bash

⚠️ Проблема 2: bash vs sh
   /bin/sh может быть dash не bash
   
   Решение:
   Использовать #!/bin/bash для bash
   Использовать #!/bin/sh для POSIX

⚠️ Проблема 3: bash-измы в sh
   Некоторые bash функции не работают в sh
   
   Решение:
   Проверять совместимость
   Использовать shellcheck

⚠️ Проблема 4: .bashrc vs .bash_profile
   Разные файлы для разных shells
   
   Решение:
   .bashrc для interactive non-login
   .bash_profile для login shells

⚠️ Проблема 5: PATH не настроен
   bash: command not found
   
   Решение:
   export PATH="/usr/local/bin:$PATH"
   Добавить в ~/.bashrc

⚠️ Проблема 6: History не работает
   История команд не сохраняется
   
   Решение:
   Проверить HISTFILE переменную
   chmod 600 ~/.bash_history

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias bashrc='vi ~/.bashrc'" >> ~/.bashrc
echo "alias bashrc='vi ~/.bashrc'" >> ~/.zshrc

echo "alias sourcebash='source ~/.bashrc'" >> ~/.bashrc
echo "alias sourcebash='source ~/.bashrc'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия Bash
bash --version

# Тест 2: Простой скрипт
echo '#!/bin/bash
echo "OK"' | bash

# Тест 3: Арифметика
echo 'echo $((2 + 2))' | bash

# Тест 4: Arrays
echo 'ARR=(1 2 3); echo ${ARR[0]}' | bash

# Тест 5: Functions
echo 'func() { echo "OK"; }; func' | bash

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ УТИЛИТЫ
================================================================================

# Базовые утилиты:

# ShellCheck (линтер)
sudo apt install shellcheck
# https://www.shellcheck.net/

# shfmt (форматирование)
go install mvdan.cc/sh/v3/cmd/shfmt@latest

# bash-completion (автодополнение)
sudo apt install bash-completion

# Утилиты:
# bash (shell)
# sh (POSIX shell)
# dash (Debian Almquist Shell)

================================================================================
                         КОНЕЦ README_BASH
================================================================================
