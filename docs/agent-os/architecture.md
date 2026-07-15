# Архитектура Agent OS

## Базовый принцип

Agent OS — не второй независимый Hermes на Windows. Это один Hermes backend на Mac mini и два клиента Hermes Desktop: macOS и Windows.

```text
macOS Desktop ─┐
               ├─> Hermes backend на Mac mini ─> профили, память, сессии, gateway
Windows Desktop ┘                              └> SSH/backend Windows для проектного кода
```

## Распределение ответственности

| Слой | Где работает | Назначение |
|---|---|---|
| Hermes backend | Mac mini | Единый источник профилей, памяти, сессий, Telegram gateway и интеграций |
| Hermes Desktop для macOS | Mac mini | Локальный клиент к backend |
| Hermes Desktop для Windows | Windows | Основной пользовательский интерфейс Вадима |
| Код проектов | Windows | Web/Core/Android-разработка и проектные рабочие папки |
| iOS/Xcode | Mac mini | Сборка и работа с iOS |

## Исходный код и обновления

Весь исходный код Hermes Desktop и наши изменения находятся в этом репозитории `agent-os`. Оригинальный `NousResearch/hermes-agent` остаётся внешним источником обновлений.

Порядок обновления:

1. Получить новую версию оригинального Hermes.
2. Внести её в `agent-os`.
3. Разрешить конфликты с нашими UI-изменениями.
4. Проверить Desktop на macOS и Windows.
5. Собрать и выпустить одинаковую версию для обеих платформ.
