---
tags:
  - type/note
source:
related:
  - "[[Game Development]]"
  - "[[SFML]]"
area:
up:
  - "[[MOC - C++ Language]]"
---
Полное руководство по созданию нового проекта на [[MOC - C++ Language|C++]] с использованием:
- Zed editor
- CMake + Ninja
- SFML 2.6 (через Homebrew)
 
---
## 1. Установка зависимостей

```bash
brew install cmake ninja sfml@2
````

Проверить путь к SFML:

```
brew --prefix sfml@2
```

---

## **2. Создание структуры проекта**

```
my-sfml-app/
├── .zed/
│   ├── settings.json
│   └── tasks.json
├── build/
├── CMakeLists.txt
└── src/
    └── main.cpp
```

---

## **3. CMakeLists.txt**

```
cmake_minimum_required(VERSION 3.20)
project(my_sfml_app LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

find_package(SFML 2.6 COMPONENTS system window graphics audio network REQUIRED)

add_executable(my_sfml_app
    src/main.cpp
)

target_link_libraries(my_sfml_app PRIVATE
    sfml-system
    sfml-window
    sfml-graphics
    sfml-audio
    sfml-network
)
```

---

## **4. main.cpp**

```
#include <SFML/Graphics.hpp>

int main() {
    sf::RenderWindow window(sf::VideoMode(800, 600), "SFML App");

    sf::CircleShape shape(80.f);
    shape.setPosition(200.f, 150.f);

    while (window.isOpen()) {
        sf::Event event{};
        while (window.pollEvent(event)) {
            if (event.type == sf::Event::Closed)
                window.close();
        }

        window.clear();
        window.draw(shape);
        window.display();
    }

    return 0;
}
```

---

## **5. Первый билд**

```
cmake -S . -B build -G Ninja \
  -DCMAKE_BUILD_TYPE=Debug \
  -DCMAKE_PREFIX_PATH="$(brew --prefix sfml@2)"

cmake --build build
```

Запуск:

```
./build/my_sfml_app
```

---

## **6. Настройка Zed Tasks**

.zed/tasks.json:

```
[
  {
    "label": "cmake configure",
    "command": "cmake",
    "args": [
      "-S", ".",
      "-B", "build",
      "-G", "Ninja",
      "-DCMAKE_BUILD_TYPE=Debug",
      "-DCMAKE_PREFIX_PATH=/opt/homebrew/opt/sfml@2"
    ]
  },
  {
    "label": "build",
    "command": "cmake",
    "args": ["--build", "build"]
  },
  {
    "label": "run",
    "command": "./build/my_sfml_app"
  }
]
```

> Для Intel Mac используйте путь:

> /usr/local/opt/sfml@2

---

## **7. Настройки Zed (опционально)**

.zed/settings.json:

```
{
  "languages": {
    "C++": {
      "format_on_save": "on",
      "tab_size": 4
    }
  }
}
```

---

## **8. .gitignore**

```
# Build
build/
cmake-build-*/

# CMake
CMakeCache.txt
CMakeFiles/
cmake_install.cmake
install_manifest.txt

# Ninja
.ninja_deps
.ninja_log
build.ninja

# Binaries
*.exe
*.out
*.app
*.dSYM
*.o
*.a
*.so
*.dylib

# macOS
.DS_Store

# Editors
.vscode/
.idea/
```

> .zed/ рекомендуется оставить в репозитории (там tasks и настройки проекта)

---

## **9. Проверка зависимостей**

```
otool -L build/my_sfml_app
```

---

## **10. Важно понимать**

- Используется **динамическая линковка (.dylib)**
- Библиотеки берутся из Homebrew
- Для разработки ничего дополнительно делать не нужно
- Для распространения потребуется .app bundle или настройка rpath

---

## **11. Быстрый workflow**

```
# configure
cmake -S . -B build -G Ninja -DCMAKE_PREFIX_PATH="$(brew --prefix sfml@2)"

# build
cmake --build build

# run
./build/my_sfml_app
```

---

## **12. Полезные команды**

```
# очистить билд
rm -rf build

# пересобрать
cmake --build build --clean-first

# verbose build
cmake --build build --verbose
```