================================================================================
                    SCALA - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         JVM + OOP + Functional Programming + 20+ лет эволюции
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка Scala (sbt/coursier)
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами (sbt/coursier)
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые библиотеки

================================================================================
1. УСТАНОВКА SCALA
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    SCALA = JVM + OOP + FUNCTIONAL PROGRAMMING                │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  Scala используется:                                                         │
│  • Enterprise applications                                                  │
│  • Big Data (Apache Spark)                                                  │
│  • Functional programming на JVM                                            │
│  • Web development (Play Framework)                                         │
│  • Distributed systems                                                      │
│                                                                              │
│  • Работает на JVM (и Scala.js для JS)                                      │
│  • 20+ лет развития (2004-2024)                                             │
│  • Объектно-ориентированный + функциональный                                │
│  • Статическая типизация с inference                                        │
│  • Совместимость с Java                                                     │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Через coursier (рекомендуется!)
curl -fL https://github.com/coursier/launchers/raw/master/cs-x86_64-pc-linux.gz | gzip -d > cs
chmod +x cs
./cs setup

# Или через sbt
echo "deb https://repo.scala-sbt.org/scalasbt/debian all main" | sudo tee /etc/apt/sources.list.d/sbt.list
curl -sL "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x2EE0EA64E40A89B84B2DF73499E82A75642AC823" | sudo apt-key add
sudo apt update
sudo apt install sbt

# Проверка
scala --version
sbt --version

macOS (Homebrew):
-----------------
brew install scala
brew install sbt

# Проверка
scala --version

Windows:
--------
# Через coursier
# Скачать с https://get-coursier.io/

# Или sbt
# Скачать с https://www.scala-sbt.org/download.html

# Проверка в PowerShell:
scala --version

Docker (универсально):
----------------------
docker run -it --rm hseeberger/scala-sbt scala --version

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для Scala                                           │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ IntelliJ IDEA   │ ★★★★★ - Лучшая для Scala (Scala plugin)                   │
│ VS Code         │ ★★★★★ - С Metals extension (отличная поддержка)           │
│ Vim/Neovim      │ ★★★★☆ - С coc-metals                                       │
│ Emacs           │ ★★★★☆ - С lsp-mode + metals                                │
│ Eclipse         │ ★★★☆☆ - С Scala IDE (устаревает)                          │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка IntelliJ IDEA + Scala:
--------------------------------
1. Скачать с https://www.jetbrains.com/idea/
2. Установить Scala plugin
3. Создать Scala проект

Установка VS Code + Metals:
---------------------------
1. Extensions (Ctrl+Shift+X)
2. Установить: "Metals" от Scala Center
3. Автоматическая настройка

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# Scala REPL
scala

# В REPL:
scala> val x = 5
scala> println(x)
scala> :quit  # Выход

# Создание проекта
sbt new scala/scala-seed.g8

# Структура проекта:
my_project/
├── build.sbt        # Build конфигурация
├── src/
│   └── main/
│       └── scala/
│           └── Main.scala
└── project/
    └── build.properties

# Простая программа (Main.scala)
object Main {
  def main(args: Array[String]): Unit = {
    println("Hello, Scala!")
  }
}

# Компиляция и запуск
sbt run

# Компиляция в JAR
sbt package

# Scala.js (компиляция в JavaScript)
sbt fastOptJS

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ (SBT/COURSIER)
================================================================================

# sbt (Scala Build Tool)
# build.sbt файл:
name := "MyProject"
version := "1.0.0"
scalaVersion := "2.13.10"

libraryDependencies += "org.scalatest" %% "scalatest" % "3.2.15" % Test

# coursiier (альтернатива)
cs launch scala:2.13.10

# Популярные библиотеки:
# akka (actor model)
# cats (functional programming)
# scalatest (testing)
# play (web framework)
# spark (big data)

# Установка зависимостей
sbt update

# Запуск с зависимостями
sbt run

# Публикация библиотеки
sbt publish

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: Java версия
   Scala требует JDK 8+
   
   Решение:
   java -version
   export JAVA_HOME=/usr/lib/jvm/java-11-openjdk

⚠️ Проблема 2: sbt медленный первый запуск
   Первый запуск загружает зависимости
   
   Решение:
   Это нормально - последующие запуски быстрее
   Использовать offline mode после первого раза

⚠️ Проблема 3: Scala 2 vs Scala 3
   Scala 3 (Dotty) имеет breaking changes
   
   Решение:
   Использовать Scala 2.13 для совместимости
   Или Scala 3 для новых проектов

⚠️ Проблема 4: Память JVM
   sbt может потреблять много памяти
   
   Решение:
   export SBT_OPTS="-Xmx2G"
   Добавить в ~/.sbtconfig

⚠️ Проблема 5: Конфликты зависимостей
   Разные версии библиотек
   
   Решение:
   sbt dependencyTree
   Использовать dependencyOverrides

⚠️ Проблема 6: Compile time
   Scala компиляция может быть медленной
   
   Решение:
   Использовать incremental compilation
   sbt ~run для watch mode

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias scala='scala'" >> ~/.bashrc
echo "alias scala='scala'" >> ~/.zshrc

echo "alias sbt='sbt'" >> ~/.bashrc
echo "alias sbt='sbt'" >> ~/.zshrc

echo "alias scalac='scalac'" >> ~/.bashrc
echo "alias scalac='scalac'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия Scala
scala --version

# Тест 2: Версия sbt
sbt --version

# Тест 3: Простая программа
echo 'object Test { def main(args: Array[String]): Unit = { println("OK") } }' > Test.scala
scalac Test.scala
scala Test
rm Test.scala Test.class

# Тест 4: sbt проект
sbt new scala/scala-seed.g8
cd scala-seed
sbt run
cd ..
rm -rf scala-seed

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ БИБЛИОТЕКИ
================================================================================

# Базовые библиотеки (build.sbt):

# Testing
libraryDependencies += "org.scalatest" %% "scalatest" % "3.2.15" % Test

# Functional programming
libraryDependencies += "org.typelevel" %% "cats-core" % "2.9.0"

# JSON
libraryDependencies += "com.lihaoyi" %% "upickle" % "2.0.0"

# HTTP client
libraryDependencies += "io.circe" %% "circe-core" % "0.14.3"

# Database
libraryDependencies += "org.typelevel" %% "doobie-core" % "1.0.0-RC2"

# Web framework
libraryDependencies += "com.typesafe.play" %% "play" % "2.8.18"

# Big Data
libraryDependencies += "org.apache.spark" %% "spark-core" % "3.3.1"

# Akka (actor model)
libraryDependencies += "com.typesafe.akka" %% "akka-actor" % "2.6.20"

================================================================================
                         КОНЕЦ README_SCALA
================================================================================
