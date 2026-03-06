================================================================================
                    JAVA - СРЕДА РАЗРАБОТКИ И УСТАНОВКА
                         Enterprise + JVM + 25+ лет эволюции
================================================================================

ОГЛАВЛЕНИЕ:
-----------
1. Установка Java (JDK)
2. Редакторы и IDE
3. Быстрый старт
4. Управление пакетами (Maven/Gradle)
5. Подводные камни установки
6. Алиасы для терминала
7. Проверка работоспособности
8. Рекомендуемые библиотеки

================================================================================
1. УСТАНОВКА JAVA (JDK)
================================================================================

┌──────────────────────────────────────────────────────────────────────────────┐
│                    JAVA = JVM + 25+ ЛЕТ ЭВОЛЮЦИИ                             │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  Java компилируется в байт-код (JVM):                                        │
│  • Кроссплатформенность (Write Once, Run Anywhere)                          │
│  • JIT компиляция (runtime оптимизации)                                     │
│  • GC (автоматическое управление памятью)                                   │
│  • Огромная экосистема (Maven Central = 3+ млн артефактов)                  │
│                                                                              │
│  Версии: LTS (11, 17, 21) или Latest (22+)                                  │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

Linux (Ubuntu/Debian):
----------------------
# Вариант 1: Через SDKMAN (рекомендуется!)
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
sdk install java 21.0.2-tem
sdk use java 21.0.2-tem

# Вариант 2: Через apt
sudo apt update
sudo apt install openjdk-21-jdk

# Проверка
java --version
javac --version

macOS (Homebrew):
-----------------
brew install openjdk@21

# Проверка
java --version

Windows:
--------
# Скачать с https://adoptium.net/
# Установщик .exe
# Добавить в PATH: C:\Program Files\Eclipse Adoptium\jdk-21\bin

# Проверка в PowerShell:
java --version

Docker (универсально):
----------------------
docker run -it --rm eclipse-temurin:21 java --version

================================================================================
2. РЕДАКТОРЫ И IDE
================================================================================

┌─────────────────┬────────────────────────────────────────────────────────────┐
│ Редактор        │ Оценка для Java                                            │
├─────────────────┼────────────────────────────────────────────────────────────┤
│ IntelliJ IDEA   │ ★★★★★ - Лучшая IDE для Java (JetBrains)                   │
│ Eclipse         │ ★★★★☆ - Классическая IDE (бесплатная)                     │
│ VS Code         │ ★★★★☆ - С Extension Pack for Java                         │
│ NetBeans        │ ★★★☆☆ - Официальная Oracle IDE                            │
│ Vim/Neovim      │ ★★★☆☆ - С vim-java                                        │
└─────────────────┴────────────────────────────────────────────────────────────┘

Установка IntelliJ IDEA:
------------------------
# Community Edition (бесплатная)
# Ultimate Edition (платная, есть для студентов)

# Скачать с https://www.jetbrains.com/idea/

Установка VS Code + Java:
-------------------------
1. Extensions (Ctrl+Shift+X)
2. Установить: "Extension Pack for Java" от Microsoft
3. Установить: "Spring Boot Extension Pack" (если нужно)

================================================================================
3. БЫСТРЫЙ СТАРТ
================================================================================

# Создание проекта (Maven)
mvn archetype:generate -DgroupId=com.example -DartifactId=my_project -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

# Создание проекта (Gradle)
gradle init --type basic

# Структура проекта (Maven):
my_project/
├── pom.xml            # Конфигурация Maven
├── src/
│   ├── main/
│   │   └── java/
│   │       └── com/
│   │           └── example/
│   │               └── App.java
│   └── test/
│       └── java/
└── target/            # Скомпилированные файлы

# Компиляция
javac src/App.java

# Запуск
java App

# Maven сборка
mvn clean compile
mvn clean package
mvn clean install

# Gradle сборка
gradle build
gradle run

# JAR файл
jar cf app.jar *.class

# Запуск JAR
java -jar app.jar

# Модули (Java 9+)
jmod create my_module.jmod --class-path classes

================================================================================
4. УПРАВЛЕНИЕ ПАКЕТАМИ (MAVEN/GRADLE)
================================================================================

# Maven (pom.xml):
<dependencies>
    <dependency>
        <groupId>org.apache.commons</groupId>
        <artifactId>commons-lang3</artifactId>
        <version>3.14.0</version>
    </dependency>
</dependencies>

# Maven команды:
mvn dependency:tree      # Показать зависимости
mvn dependency:resolve   # Разрешить зависимости
mvn clean                # Очистить
mvn compile              # Скомпилировать
mvn test                 # Тесты
mvn package              # Создать JAR/WAR
mvn install              # Установить в локальный репозиторий
mvn deploy               # Развернуть в репозиторий

# Gradle (build.gradle):
dependencies {
    implementation 'org.apache.commons:commons-lang3:3.14.0'
    testImplementation 'org.junit:junit:5.10.0'
}

# Gradle команды:
gradle dependencies      # Показать зависимости
gradle build             # Собрать
gradle test              # Тесты
gradle clean             # Очистить

# Поиск пакетов:
# https://mvnrepository.com/
# https://search.maven.org/

================================================================================
5. ПОДВОДНЫЕ КАМНИ УСТАНОВКИ
================================================================================

⚠️ Проблема 1: JAVA_HOME не установлен
   java: command not found
   
   Решение:
   export JAVA_HOME=/usr/lib/jvm/java-21-openjdk
   export PATH=$JAVA_HOME/bin:$PATH
   Добавить в ~/.bashrc

⚠️ Проблема 2: Конфликт версий
   Разные проекты требуют разные версии
   
   Решение: SDKMAN manage версии
   sdk install java 17.0.2-tem
   sdk use java 17.0.2-tem
   sdk default java 17.0.2-tem

⚠️ Проблема 3: Maven/Gradle не найдены
   mvn: command not found
   
   Решение:
   sdk install maven
   sdk install gradle

⚠️ Проблема 4: Encoding проблемы
   Кириллица не отображается
   
   Решение:
   Добавить -Dfile.encoding=UTF-8
   Или: export JAVA_TOOL_OPTIONS="-Dfile.encoding=UTF-8"

⚠️ Проблема 5: Память JVM
   OutOfMemoryError
   
   Решение:
   java -Xmx2g -Xms512m App

⚠️ Проблема 6: Модули (Java 9+)
   Module not found
   
   Решение:
   Проверить module-info.java
   Или использовать --add-modules

================================================================================
6. АЛИАСЫ ДЛЯ ТЕРМИНАЛА
================================================================================

# Добавить в ~/.bashrc, ~/.zshrc, ~/.mkshrc

echo "alias j='java'" >> ~/.bashrc
echo "alias j='java'" >> ~/.zshrc

echo "alias jc='javac'" >> ~/.bashrc
echo "alias jc='javac'" >> ~/.zshrc

echo "alias mvn='mvn'" >> ~/.bashrc
echo "alias mvn='mvn'" >> ~/.zshrc

echo "alias mvnc='mvn clean'" >> ~/.bashrc
echo "alias mvnc='mvn clean'" >> ~/.zshrc

echo "alias mvnt='mvn test'" >> ~/.bashrc
echo "alias mvnt='mvn test'" >> ~/.zshrc

echo "alias gradle='gradle'" >> ~/.bashrc
echo "alias gradle='gradle'" >> ~/.zshrc

# Применить изменения
source ~/.bashrc
source ~/.zshrc
source ~/.mkshrc 2>/dev/null || true

================================================================================
7. ПРОВЕРКА РАБОТОСПОСОБНОСТИ
================================================================================

# Тест 1: Версия Java
java --version

# Тест 2: Версия компилятора
javac --version

# Тест 3: Простое вычисление
echo 'class Test { public static void main(String[] args) { System.out.println(2 + 2); } }' > Test.java
javac Test.java
java Test
rm Test.java Test.class

# Тест 4: Maven проект
mvn archetype:generate -DgroupId=test -DartifactId=test -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
cd test
mvn test
cd ..
rm -rf test

# Если все тесты прошли → установка успешна!

================================================================================
8. РЕКОМЕНДУЕМЫЕ БИБЛИОТЕКИ
================================================================================

# Базовые зависимости (pom.xml):

<dependencies>
    # Утилиты
    <dependency>
        <groupId>org.apache.commons</groupId>
        <artifactId>commons-lang3</artifactId>
        <version>3.14.0</version>
    </dependency>
    
    # Collections
    <dependency>
        <groupId>com.google.guava</groupId>
        <artifactId>guava</artifactId>
        <version>33.0.0-jre</version>
    </dependency>
    
    # JSON
    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-databind</artifactId>
        <version>2.16.0</version>
    </dependency>
    
    # Логирование
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>2.0.0</version>
    </dependency>
    
    # Тестирование
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter</artifactId>
        <version>5.10.0</version>
        <scope>test</scope>
    </dependency>
    
    # HTTP клиент
    <dependency>
        <groupId>org.apache.httpcomponents</groupId>
        <artifactId>httpclient</artifactId>
        <version>4.5.14</version>
    </dependency>
    
    # Database
    <dependency>
        <groupId>org.hibernate</groupId>
        <artifactId>hibernate-core</artifactId>
        <version>6.4.0</version>
    </dependency>
</dependencies>

================================================================================
                         КОНЕЦ README_JAVA
================================================================================
