================================================================================
                    GO - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Simple + Fast + Concurrent + Production Ready
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка Go
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами (Go modules)
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые библиотеки

================================================================================
1. УСТАНОВКА GO
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    GO = SIMPLE + FAST + CONCURRENT                           │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  Go используется:                                                            │
│  • Backend services                                                         │
│  • Microservices                                                            │
│  • CLI tools                                                                │
│  • DevOps tools (Docker, Kubernetes написаны на Go)                         │
│  • Cloud infrastructure                                                     │
│  • Network programming                                                      │
│                                                                              │
│  • 2009+ разработка (Google)                                                │
│  • Статическая типизация                                                    │
│  • Garbage collected                                                        │
│  • Concurrent (goroutines, channels)                                        │
│  • Single binary deployment                                                 │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Вариант 1: Через официальный архив
wget https://go.dev/dl/go1.22.0.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.22.0.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin

# Вариант 2: Через apt (может быть старая версия)
sudo apt update
sudo apt install golang-go

# Проверка
go version

macOS (Homebrew):
-----------------
brew install go

# Проверка
go version

Windows:
--------
# Скачать с https://go.dev/dl/
# Установщик .exe
# Добавить в PATH: C:\Program Files\Go\bin

# Проверка в PowerShell:
go version

Docker (универсально):
----------------------
docker run -it --rm golang:latest go version

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для Go                                              │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ VS Code         │ ★★★★★ - С Go extension (официальный)                      │
│ GoLand          │ ★★★★★ - Лучшая IDE для Go (JetBrains)                     │
│ Vim/Neovim      │ ★★★★☆ - С vim-go                                            │
│ Emacs           │ ★★★★☆ - С go-mode                                             │
│ Teko            │ ★★★★☆ - Встроенная поддержка                               │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка VS Code + Go:
-----------------------
1. Extensions (Ctrl+Shift+X)
2. Установить: "Go" от Go Team at Google
3. Автоматическая настройка (go install gopls и т.д.)

Установка GoLand:
-----------------
# Скачать с https://www.jetbrains.com/go/
# Платная IDE (бесплатная для студентов)

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# Go REPL (нет официального REPL, но есть goplay/rt)
# Go компилируется напрямую

# Создание проекта
mkdir my_project && cd my_project
go mod init my_project

# Структура проекта:
my_project/
├── go.mod         # Module file
├── go.sum         # Dependencies checksum
├── main.go        # Главный файл
└── README.md      # Документация

# Простая программа (main.go)
package main

import "fmt"

func main() {
    fmt.Println("Hello, Go!")
}

# Запуск
go run main.go

# Компиляция
go build -o myapp main.go

# Запуск binary
./myapp

# Тесты
go test ./...

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ (GO MODULES)
================================================================================

# Go modules (встроено в Go 1.11+)

# Инициализация модуля
go mod init my_project

# go.mod файл:
module my_project

go 1.22

require (
    github.com/gin-gonic/gin v1.9.1
)

# Установка зависимостей
go get github.com/gin-gonic/gin

# Обновление зависимостей
go get -u ./...

# Очистка неиспользуемых
go mod tidy

# Поиск пакетов:
# https://pkg.go.dev/
# https://github.com/

# Популярные пакеты:
# - gin (web framework)
# - cobra (CLI tools)
# - testify (testing)
# - zap (logging)
# - gorm (ORM)

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: GOPATH vs Go modules
   Старые туториалы используют GOPATH
   
   Решение:
   Используйте Go modules (go mod init)
   Игнорируйте GOPATH для новых проектов

⚠️ Проблема 2: Версия Go
   Разные проекты требуют разные версии
   
   Решение:
   Используйте go.mod для указания версии
   Или используйте goenv для управления версиями

⚠️ Проблема 3: CGO зависимости
   Некоторые пакеты требуют C компилятор
   
   Решение:
   sudo apt install build-essential
   Или используйте CGO_ENABLED=0 для статической сборки

⚠️ Проблема 4: Go proxy
   Проблемы с загрузкой зависимостей в некоторых регионах
   
   Решение:
   export GOPROXY=https://goproxy.io,direct
   Или используйте proxy.golang.org

⚠️ Проблема 5: Binary size
   Статическая линковка увеличивает размер
   
   Решение:
   go build -ldflags="-s -w" для уменьшения
   Или используйте UPX для сжатия

⚠️ Проблема 6: Vendor directory
   Нужно ли коммитить vendor?
   
   Решение:
   go mod vendor для создания
   Коммитьте если нужна reproducible сборка

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias go='go'" >> ~/.bashrc
echo "alias go='go'" >> ~/.zshrc

echo "alias gorun='go run'" >> ~/.bashrc
echo "alias gorun='go run'" >> ~/.zshrc

echo "alias gobuild='go build'" >> ~/.bashrc
echo "alias gobuild='go build'" >> ~/.zshrc

echo "alias gotest='go test'" >> ~/.bashrc
echo "alias gotest='go test'" >> ~/.zshrc

echo "alias gofmt='go fmt'" >> ~/.bashrc
echo "alias gofmt='go fmt'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия Go
go version

# Тест 2: Простое вычисление
echo 'package main; import "fmt"; func main() { fmt.Println(2 + 2) }' | go run -

# Тест 3: Создание модуля
go mod init test_module
go mod tidy
rm go.mod go.sum

# Тест 4: Тесты
echo 'package main; import "testing"; func TestAdd(t *testing.T) { }' > main_test.go
go test
rm main_test.go

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ БИБЛИОТЕКИ
================================================================================

# Базовые пакеты (go get):

# Web framework
go get github.com/gin-gonic/gin

# CLI tools
go get github.com/spf13/cobra

# Testing
go get github.com/stretchr/testify

# Logging
go get go.uber.org/zap

# Database
go get gorm.io/gorm

# HTTP client
go get github.com/go-resty/resty/v2

# Configuration
go get github.com/spf13/viper

# Utilities
go get github.com/pkg/errors

================================================================================
                         КОНЕЦ README_GO
================================================================================
