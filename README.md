# MTA Market — модуль

Нативный модуль MTA:SA для площадки. Два слоя в одном репозитории:

1. **SDK** — C++20-обёртка ABI MTA (типизированный Lua, async, таймеры, CLI `mta`).
2. **DRM spike** — `source/functions/drm/spike.cpp`. Проверка: зашифрованный Lua можно выполнить в VM вызывающего ресурса. Шифр демо: byte complement. Это не Guard v2.

Протокол маркета и статус: [mta-market-document](https://github.com/acc-holo-dev/mta-market-document) (раздел DRM).  
Сайт: [mta-market-site](https://github.com/acc-holo-dev/mta-market-site).

Справка SDK (английский, это API заголовков): `other/documents/` — `TUTORIAL.md`, `example.md`, `api.md`, `architecture.md`.

## Сборка и тесты

CMake 3.27+, компилятор, Python 3.11+ для CLI.

```bash
mta doctor
mta build
mta test
```

Артефакт: `.dll` / `.so` → `modules/` сервера, запись в `mtaserver.conf`.

Имя модуля задаётся в `config/module.toml` (сейчас `base` / 2.1.0).
