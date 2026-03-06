================================================================================
                    PYTHON - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Универсальный язык + 30+ лет эволюции
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка Python (pyenv/pip)
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами (pip/venv)
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые пакеты

================================================================================
1. УСТАНОВКА PYTHON (PYENV/PIP)
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    PYTHON = УНИВЕРСАЛЬНЫЙ ЯЗЫК + 30+ ЛЕТ                     │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  Python работает:                                                            │
│  • Data Science (NumPy, Pandas, Scikit-learn)                               │
│  • Web (Django, Flask, FastAPI)                                             │
│  • Автоматизация и скрипты                                                  │
│  • Машинное обучение (TensorFlow, PyTorch)                                  │
│  • DevOps и инструменты                                                     │
│                                                                              │
│  Версии: Python 3.8+ (Python 2 устарел!)                                    │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Вариант 1: Через pyenv (рекомендуется!)
curl https://pyenv.run | bash
# Добавить в ~/.bashrc:
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"

# Установить версию
pyenv install 3.12.0
pyenv global 3.12.0

# Вариант 2: Через apt (может быть старая версия)
sudo apt update
sudo apt install python3 python3-pip python3-venv

# Проверка
python3 --version
pip3 --version

macOS (Homebrew):
-----------------
brew install python@3.12

# Проверка
python3 --version

Windows:
--------
# Скачать с https://www.python.org/
# Установщик .exe
# Добавить в PATH при установке!

# Проверка в PowerShell:
python --version

Docker (универсально):
----------------------
docker run -it --rm python:3.12 python --version

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для Python                                          │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ VS Code         │ ★★★★★ - С Python extension (от Microsoft)                 │
│ PyCharm         │ ★★★★★ - Лучшая IDE для Python (JetBrains)                 │
│ Vim/Neovim      │ ★★★★☆ - С python-vim + LSP                                │
│ Emacs           │ ★★★★☆ - С python-mode + lsp                                 │
│ Jupyter         │ ★★★★★ - Для Data Science (интерактивно)                   │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка VS Code + Python:
---------------------------
1. Extensions (Ctrl+Shift+X)
2. Установить: "Python" от Microsoft
3. Установить: "Pylance" для автодополнения
4. Установить: "Jupyter" для ноутбуков

Установка PyCharm:
------------------
# Community Edition (бесплатная)
# Professional Edition (платная)
# Скачать с https://www.jetbrains.com/pycharm/

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# Создание проекта
mkdir my_project && cd my_project

# Виртуальное окружение (ОБЯЗАТЕЛЬНО!)
python3 -m venv venv
source venv/bin/activate  # Linux/macOS
# или
venv\Scripts\activate  # Windows

# Установка пакетов
pip install requests

# Запуск скрипта
python script.py

# Python REPL
python

# В REPL:
>>> 2 + 2
4
>>> exit()  # Выход

# Jupyter Notebook
jupyter notebook

# Форматирование
black script.py

# Линтинг
flake8 script.py

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ (PIP/VENV)
================================================================================

# pip (идёт с Python)
pip install package_name
pip install package_name==1.0.0  # Конкретная версия
pip install -r requirements.txt  # Из файла
pip uninstall package_name
pip list
pip freeze > requirements.txt  # Сохранить зависимости

# Виртуальное окружение (ОБЯЗАТЕЛЬНО!)
python -m venv venv
source venv/bin/activate  # Активировать
deactivate  # Деактивировать

# requirements.txt:
requests==2.31.0
numpy>=1.24.0
pandas~=2.0.0

# poetry (альтернатива pip)
curl -sSL https://install.python-poetry.org | python3 -
poetry new my_project
poetry add requests
poetry install

# pipenv (ещё одна альтернатива)
pip install pipenv
pipenv install requests
pipenv shell

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: pip требует sudo (Linux)
   pip install package → Permission denied
   
   Решение:
   python -m venv venv
   source venv/bin/activate
   pip install package  # Внутри venv!

⚠️ Проблема 2: Конфликт версий Python
   Разные проекты требуют разные версии
   
   Решение: pyenv manage версии
   pyenv install 3.10.0
   pyenv local 3.10.0  # Для конкретного проекта

⚠️ Проблема 3: Python 2 vs Python 3
   python --version может показать 2.7!
   
   Решение:
   Используйте python3 или настройте alias
   alias python=python3

⚠ Проблема 4: Зависимости не компилируются
   Некоторые пакеты требуют C компиляции
   
   Решение:
   sudo apt install build-essential python3-dev

⚠ Проблема 5: Encoding проблемы
   Кириллица не отображается
   
   Решение:
   # -*- coding: utf-8 -*-
   Или: export PYTHONIOENCODING=utf-8

⚠ Проблема 6: GIL (Global Interpreter Lock)
   Многопоточность ограничена
   
   Решение:
   Используйте multiprocessing или asyncio

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias py='python3'" >> ~/.bashrc
echo "alias py='python3'" >> ~/.zshrc

echo "alias pip='pip3'" >> ~/.bashrc
echo "alias pip='pip3'" >> ~/.zshrc

echo "alias venv='python3 -m venv'" >> ~/.bashrc
echo "alias venv='python3 -m venv'" >> ~/.zshrc

echo "alias req='pip freeze > requirements.txt'" >> ~/.bashrc
echo "alias req='pip freeze > requirements.txt'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия Python
python3 --version

# Тест 2: Версия pip
pip3 --version

# Тест 3: Простое вычисление
echo "print(2 + 2)" | python3

# Тест 4: Виртуальное окружение
python3 -m venv test_venv
source test_venv/bin/activate
pip install requests
deactivate
rm -rf test_venv

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ ПАКЕТЫ
================================================================================

# Базовые пакеты (requirements.txt):

# Data Science
numpy>=1.24.0
pandas>=2.0.0
scipy>=1.10.0
matplotlib>=3.7.0
scikit-learn>=1.2.0

# Web
requests>=2.31.0
fastapi>=0.100.0
uvicorn>=0.23.0
sqlalchemy>=2.0.0

# Утилиты
black>=23.0.0  # Форматирование
flake8>=6.0.0  # Линтинг
pytest>=7.0.0  # Тесты
mypy>=1.0.0    # Типизация

# Машинное обучение
torch>=2.0.0
tensorflow>=2.12.0

# Асинхронность
asyncio  # Встроено
aiohttp>=3.8.0

================================================================================
                         КОНЕЦ README_PYTHON
================================================================================
