# Что это?

Этот репозиторий содержит автоматически обновляемые правила маршрутизации [**V2Ray**](https://github.com/v2fly/v2ray-core), основанные на данных о доменах и IP-адресах, **доступных внутри России**.

В отличие от «списков блокировок», здесь собирается «разрешенный список»: маршрут по умолчанию должен быть `proxy`, а совпадение с доменом или адресом из файла — `direct`. Файлы получаются небольшими и удобными для роутеров, также отпадает необходимость постоянно включать/выключать VPN.

Распространяемые здесь файлы `geoip.dat` и `geosite.dat` могут использоваться в [V2Ray](https://github.com/v2fly/v2ray-core), [v2rayN](https://github.com/2dust/v2rayN), [Xray-core](https://github.com/XTLS/Xray-core), [mihomo](https://github.com/MetaCubeX/mihomo/tree/Meta), [hysteria](https://github.com/apernet/hysteria), [Trojan-Go](https://github.com/p4gefau1t/trojan-go), [leaf](https://github.com/eycorsican/leaf) и так далее.

Репозиторий обновляется каждый день в 00:30 UTC.

## Какие категории содержатся в файлах

### geoip.dat

`geoip.dat` генерируется в репозитории [@golukon/russia-only-geoip](https://github.com/golukon/russia-only-geoip). Источник данных: [scanitex.com](https://scanitex.com/ru/resources/ip-ranges/ru).

Доступные категории:

- `geoip:ru` — список всех российских IPv4-адресов
- `geoip:private` — приватные и зарезервированные сети, например `10.0.0.0/8`, `127.0.0.0/8`, `192.168.0.0/16`

### geosite.dat

`geosite.dat` генерируется в репозитории [@golukon/russia-only-geosite](https://github.com/golukon/russia-only-geosite). Данные собираются из форков [@golukon](https://github.com/golukon):

- [@golukon/domains-only-russia](https://github.com/golukon/domains-only-russia) — `ru-available-only-inside`
- [@golukon/russia-mobile-internet-whitelist](https://github.com/golukon/russia-mobile-internet-whitelist) — `whitelist.txt`
- [@golukon/domain-list-community](https://github.com/golukon/domain-list-community) — `category-gov-ru`

Доступные категории:

- `geosite:ru-inside` — домены, доступные внутри РФ (в т.ч. недоступные из-за границы, белые списки, госсервисы). Дублирование доменов отсутствует

## Пример конфигурации для v2rayA

```
default: proxy
ip(geoip:private)->direct

# write your own rules below
ip(geoip:ru)->direct
domain(geosite:ru-inside)->direct
```

## Пример конфигурации для v2rayN/v2rayNG

```
[
    {
        "enabled": true,
        "ip": [
            "geoip:private"
        ],
        "locked": false,
        "outboundTag": "direct",
        "remarks": "RU-0 [Приватные сети напрямую]"
    },
    {
        "enabled": true,
        "ip": [
            "geoip:ru"
        ],
        "locked": false,
        "outboundTag": "direct",
        "remarks": "RU-0 [Российские IPv4 напрямую]"
    },
    {
        "domain": [
            "geosite:ru-inside"
        ],
        "enabled": true,
        "locked": false,
        "outboundTag": "direct",
        "remarks": "RU-0 [Российские домены напрямую]"
    },
    {
        "enabled": true,
        "locked": false,
        "outboundTag": "proxy",
        "port": "0-65535",
        "remarks": "RU-0 [Остальное прокси]"
    }
]
```

# Cкачать

По ссылкам ниже всегда доступна последняя версия файлов.

- **geoip.dat**
    - [https://raw.githubusercontent.com/golukon/russia-v2ray-rules-lite/release/geoip.dat](https://raw.githubusercontent.com/golukon/russia-v2ray-rules-lite/release/geoip.dat)
- **geosite.dat**
    - [https://raw.githubusercontent.com/golukon/russia-v2ray-rules-lite/release/geosite.dat](https://raw.githubusercontent.com/golukon/russia-v2ray-rules-lite/release/geosite.dat)


## Cмежные проекты

- [@golukon/russia-only-geoip](https://github.com/golukon/russia-only-geoip) - генерация geoip файлов
- [@golukon/russia-only-geosite](https://github.com/golukon/russia-only-geosite) - генерация geosite файлов

## Благодарности

- [scanitex.com](https://scanitex.com/ru/resources/ip-ranges/ru) - за список российских IP-адресов
- [@Loyalsoldier/geoip](https://github.com/Loyalsoldier/geoip) - за сборщик geoip.dat
- [@v2fly/domain-list-community](https://github.com/v2fly/domain-list-community) - за сборщик geosite.dat и `category-gov-ru`
- [@runetfreedom/russia-domains-list](https://github.com/runetfreedom/russia-domains-list) - за список `ru-available-only-inside` и шаблоны репозиториев
- [@hxehex/russia-mobile-internet-whitelist](https://github.com/hxehex/russia-mobile-internet-whitelist) - за список `whitelist.txt`
