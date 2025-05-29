---
brief: В этом руководстве описывается работа с Defold SDK при создании нативных расширений.
github: https://github.com/defold/doc
language: ru
layout: manual
title: Нативные расширения - Defold SDK
toc:
- Defold SDK
- Использование
---

# Defold SDK

Defold SDK содержит необходимую функциональность для объявления нативного расширения, а также взаимодействия с низкоуровневым нативным слоем платформы, на котором работает приложение, и высокоуровневым слоем Lua, в котором создается игровая логика.

## Использование

Используете Defold SDK, включив заголовочный файл `dmsdk/sdk.h`:

    #include <dmsdk/sdk.h>

Доступные функции SDK документированы в [API reference](/ref/overview_cpp).

Если вам нужен заголовочный файл `dmsdk/sdk.h` для кода в выбранном вами редакторе, его можно найти [здесь в основном репозитории GitHub для Defold](https://github.com/defold/defold/blob/dev/engine/sdk/src/dmsdk/sdk.h) с [заголовочными файлами для отдельных пространств имен](https://github.com/defold/defold/tree/dev/engine/dlib/src/dmsdk/dlib).