# RodinaVPN Subscription Page

Кастомная страница подписки для панели [Remnawave](https://github.com/remnawave) в стиле RodinaVPN.

**Особенности:**
- Тёмная и светлая тема с переключателем
- 5 языков: RU / EN / ZH / FA (RTL) / FR
- Анимированные искры на фоне
- Карточки: трафик с прогресс-баром, тариф, срок, устройства
- Подключение только через Happ (deep link / Crypt4Link)
- Пошаговая инструкция по платформам: iOS, Android, Windows, macOS, Apple TV, Android TV
- Кнопки: канал, чат, бот, поддержка, личный кабинет

---

## Установка

### Шаг 1 — Скачать страницу

```bash
curl -o index.html https://raw.githubusercontent.com/onetone1488-svg/rodinavpn-subpage/main/index.html
```

Или через `wget`:

```bash
wget -O index.html https://raw.githubusercontent.com/onetone1488-svg/rodinavpn-subpage/main/index.html
```

Положи файл рядом с `docker-compose.yml` (обычно `/opt/remnawave/`).

### Шаг 2 — Добавить volume в docker-compose.yml

```yaml
services:
  remnawave-subscription-page:
    image: remnawave/subscription-page:latest
    volumes:
      - ./index.html:/opt/app/frontend/index.html
    # остальные настройки без изменений
```

### Шаг 3 — Перезапустить контейнер

```bash
cd /opt/remnawave
docker compose up -d remnawave-subscription-page
```

### Шаг 4 — Загрузить app-config.json

В панели Remnawave → **Subscription Page** → **Subpage Builder** → импортировать `app-config.json` из этого репозитория (только Happ на всех платформах).

---

## Кастомизация

Открой `index.html` в редакторе и найди блок `ACTIONS` — там ссылки на канал, чат, бота и поддержку:

```js
const ACTIONS = [
  { key: 'channel', url: 'https://t.me/RVPN_Channel', ... },
  { key: 'chat',    url: 'https://t.me/RodinaVPN_Chat', ... },
  { key: 'bot',     url: 'https://t.me/rodinadl_bot', ... },
  { key: 'support', url: 'https://t.me/Milena_rvpn', ... }
];
```

Также замени ссылку на личный кабинет:

```html
<a class="cabinet-link" id="cabinet-link" href="https://cabinet.rodinavpn.tech" ...>
```

Логотип подтягивается из `brandingSettings.logoUrl` в `app-config.json` — вставь туда URL своего SVG/PNG.

---

## Скриншоты

| Тёмная тема | Светлая тема |
|---|---|
| ![dark](https://i.imgur.com/placeholder_dark.png) | ![light](https://i.imgur.com/placeholder_light.png) |

---

## Основано на

- [remnawave/subscription-page](https://github.com/remnawave/subscription-page)
- Вдохновлено [legiz-ru/Orion](https://github.com/legiz-ru/Orion)
