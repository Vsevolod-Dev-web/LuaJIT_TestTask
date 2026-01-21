# LuaJIT Test task by Vsevolod Polyakov
# Исправление ошибки сборки

## Задача: Исправвить ошибки, выпустить патч.

### Проблема num. 1

В файле lj_tab.c не установлена зависимость с заголовочным файлом `<limits.h>`
где объявлена используемая в условном операторе константа `INT_MAX`.

### Решение

    1. Переходим к файлу с ошибкой.
    2. Добавляем зависимость `#include <limits.h>`
    3. Собираем билд.
    4. Успешно.

Получаем сообщение `OK Successfully built LuaJIT`, что говорит об успешной
сборке. 

Провверим работает ли LuaJIT. Находясь в директории LuaJIT-2.1.0.-beta3/src
выполняем следующее: `./luajit -v`

Получаем сообщение: LuaJIT 2.1.0-beta3 -- Copyright (C) 2005-2017 Mike Pall. http://luajit.org/
что значит, что все работает. 

### Создание патча

Находясь в корне проекта `~/LuaJIT_TestTask` 

Создаем патч, сравнивая исправленную версию с оригиналом
```bash
diff -u original_sources/LuaJIT-2.1.0-beta3/src/lj_tab.c \
        patched_sources/LuaJIT-2.1.0-beta3/src/lj_tab.c > patches/lj_tab_fix.patch
```

Патч готов.

