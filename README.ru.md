# sing-box для Keenetic / Netcraze

Сборки sing-box для роутеров Keenetic и Netcraze.

Это не исходный код upstream `sing-box`, а релизный проект для сборки готовых бинарников под архитектуры, которые обычно используются в маршрутизаторах семейства Keenetic / Netcraze. Основная цель — собрать sing-box с нужными тегами и опубликовать готовые артефакты в GitHub Releases.

[English version](README.md)

## Что это за проект

Репозиторий автоматически:

- получает нужную версию upstream `SagerNet/sing-box` по тегу;
- собирает бинарники под целевые архитектуры;
- добавляет необходимые `build tags`;
- при необходимости сжимает бинарники с помощью `UPX`;
- публикует результаты в GitHub Releases.

## Поддерживаемые сборки

В GitHub Actions собираются бинарники для следующих конфигураций:

- `linux/arm64` + `musl`
- `linux/mipsle` + `softfloat` + `musl`
- `linux/mips` + `softfloat`

Для `arm64` и `mipsle` дополнительно включаются теги:

- `with_naive_outbound`
- `with_musl`

Для всех сборок используется набор общих тегов:

- `with_quic`
- `with_utls`
- `with_clash_api`
- `badlinkname`
- `tfogo_checklinkname0`
- `with_gvisor` для стабильных релизов

UPX-версии публикуются с суффиксом `_upx`.

## Лицензия

Проект распространяется под лицензией MIT. См. [LICENSE](LICENSE).