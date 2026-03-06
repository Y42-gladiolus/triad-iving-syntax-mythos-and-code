================================================================================
                    RUBY - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Developer Happiness + Productivity + Elegant Syntax
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка Ruby (rbenv/rvm)
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами (RubyGems/Bundler)
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые библиотеки

================================================================================
1. УСТАНОВКА RUBY
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    RUBY = DEVELOPER HAPPINESS + PRODUCTIVITY                 │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  Ruby используется:                                                          │
│  • Web development (Ruby on Rails)                                          │
│  • Scripting и automation                                                   │
│  • CLI tools                                                                │
│  • Prototyping                                                              │
│  • DevOps инструменты                                                       │
│                                                                              │
│  • 1995+ разработка                                                         │
│  • Написан на C (MRI)                                                       │
│  • Dynamic typing                                                           │
│  • Garbage collected                                                        │
│  • Elegant syntax                                                           │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Вариант 1: Через rbenv (рекомендуется!)
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
source ~/.bashrc

rbenv install 3.2.0
rbenv global 3.2.0

# Вариант 2: Через apt (может быть старая версия)
sudo apt update
sudo apt install ruby ruby-dev

# Проверка
ruby --version
gem --version

macOS (Homebrew):
-----------------
brew install ruby rbenv

# Проверка
ruby --version

Windows:
--------
# RubyInstaller
# Скачать с https://rubyinstaller.org/
# Установщик .exe включает DevKit

# Проверка в PowerShell:
ruby --version

Docker (универсально):
----------------------
docker run -it --rm ruby:latest ruby --version

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для Ruby                                            │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ VS Code         │ ★★★★★ - С Ruby extension (официальный)                    │
│ RubyMine        │ ★★★★★ - Лучшая IDE для Ruby (JetBrains)                   │
│ Vim/Neovim      │ ★★★★☆ - С ruby.vim                                         │
│ Emacs           │ ★★★★☆ - С ruby-mode                                          │
│ Sublime Text    │ ★★★★☆ - С Ruby package                                      │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка VS Code + Ruby:
-------------------------
1. Extensions (Ctrl+Shift+X)
2. Установить: "Ruby" от Peng Lv
3. Установить: "Ruby LSP" от Shopify
4. Установить: "Rubocop" для linting

Установка RubyMine:
-------------------
# Скачать с https://www.jetbrains.com/ruby/
# Платная IDE (бесплатная для студентов)

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# Ruby REPL (IRB)
irb

# В IRB:
>> 2 + 2
=> 4
>> exit  # Выход

# Создание проекта
mkdir my_project && cd my_project

# Структура проекта:
my_project/
├── main.rb        # Главный файл
├── Gemfile        # Зависимости
└── README.md      # Документация

# Простая программа (main.rb)
puts "Hello, Ruby!"

# Запуск
ruby main.rb

# IRB с файлом
irb -r ./main.rb

# Shebang
#!/usr/bin/env ruby
puts "Hello!"

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ (RUBYGEMS/BUNDLER)
================================================================================

# RubyGems (package manager)
gem install gem_name
gem uninstall gem_name
gem list
gem update

# Bundler (dependency management)
bundle install
bundle update
bundle exec ruby script.rb

# Gemfile:
source 'https://rubygems.org'

ruby '3.2.0'

gem 'rails', '~> 7.0'
gem 'pg', '~> 1.5'
gem 'puma', '~> 6.0'

group :development, :test do
  gem 'rspec-rails'
  gem 'rubocop'
end

# Поиск пакетов:
# https://rubygems.org/

# Популярные гемы:
# - rails (web framework)
# - rspec (testing)
# - rubocop (linting)
# - sidekiq (background jobs)
# - devise (authentication)

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: System Ruby vs rbenv/rvm
   Не используйте sudo gem install!
   
   Решение:
   Используйте rbenv или rvm
   Или используйте bundle install --path

⚠️ Проблема 2: Конфликт версий
   Разные проекты требуют разные версии
   
   Решение:
   rbenv local 3.2.0  # Для конкретного проекта
   Или используйте .ruby-version файл

⚠️ Проблема 3: Native extensions
   Некоторые гемы требуют компиляции
   
   Решение:
   sudo apt install build-essential libssl-dev

⚠️ Проблема 4: Gem permissions
   Permission denied ошибки
   
   Решение:
   Не используйте sudo gem install
   Используйте rbenv/rvm

⚠️ Проблема 5: Slow gem install
   Медленная установка гемов
   
   Решение:
   gem install gem_name --no-document
   Или настройте gem sources

⚠️ Проблема 6: Bundle exec
   Забыли bundle exec
   
   Решение:
   bundle exec ruby script.rb
   Или используйте binstubs

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias rb='ruby'" >> ~/.bashrc
echo "alias rb='ruby'" >> ~/.zshrc

echo "alias irb='irb'" >> ~/.bashrc
echo "alias irb='irb'" >> ~/.zshrc

echo "alias be='bundle exec'" >> ~/.bashrc
echo "alias be='bundle exec'" >> ~/.zshrc

echo "alias bi='bundle install'" >> ~/.bashrc
echo "alias bi='bundle install'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия Ruby
ruby --version

# Тест 2: Версия gem
gem --version

# Тест 3: Простое вычисление
echo "puts 2 + 2" | ruby

# Тест 4: IRB
echo "exit" | irb

# Тест 5: Gem installation
gem install rake
rake --version

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ БИБЛИОТЕКИ
================================================================================

# Базовые гемы (Gemfile):

# Web framework
gem 'rails', '~> 7.0'
gem 'sinatra'

# Database
gem 'pg', '~> 1.5'
gem 'mysql2'
gem 'sqlite3'

# Testing
gem 'rspec', '~> 3.12'
gem 'minitest'

# Linting
gem 'rubocop'

# Background jobs
gem 'sidekiq'

# Authentication
gem 'devise'

# HTTP client
gem 'httparty'
gem 'faraday'

# JSON
gem 'json'

# Utilities
gem 'pry'  # Better REPL
gem 'dotenv'  # Environment variables

================================================================================
                         КОНЕЦ README_RUBY
================================================================================
