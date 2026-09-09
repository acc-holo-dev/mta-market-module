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

## DRM client subsystem (PLAN Block 6 / H)

The module ships a real DRM client subsystem (`source/drm/`) that talks the
frozen DRM Protocol v2 of `mta-market-site`: installation identity with an
Ed25519 keypair stored in the secure key store, challenge verification,
signed-lease activation/verification/renewal, heartbeats, and lease-gated
DEK release for AES-256-GCM encrypted resources. See
`docs/H-001-inventory.md` for the full inventory and cross-platform matrix.

Build and run the standalone DRM unit tests (no MTA server required):

```sh
make -f source/drm/Makefile test
```
