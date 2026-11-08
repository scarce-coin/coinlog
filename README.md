# Монеты с выставки — офлайн-приложение (PWA)

## Файлы
index.html, manifest.webmanifest, sw.js, icon-192.png, icon-512.png — положить в одну папку на любом https-хостинге.

## Установка через GitHub Pages (один раз, ~5 минут)
1. github.com → New repository, имя например `coinlog`, Public → Create.
2. Add file → Upload files → перетащить 5 файлов → Commit.
3. Settings → Pages → Source: "Deploy from a branch", Branch: main / (root) → Save.
4. Через 1–2 минуты адрес: https://<логин>.github.io/coinlog/
5. На телефоне открыть адрес в Chrome → меню ⋮ → «Добавить на главный экран» (или «Установить приложение»).
После этого приложение работает без интернета.

## Обновление приложения
Заменить index.html в репозитории и в sw.js поменять `coinlog-v1` на `coinlog-v2` (иначе телефон будет держать старую версию в кэше).

## Рабочий цикл
- На выставке: + → фото аверса и реверса (обязательно) → размеры, вес, цена, продавец → Сохранить. Валюта, продавец и выставка подставляются с прошлой монеты.
- Вечером: ☰ → «Экспорт всего (zip)» → отправить в чат с Claude для атрибуции.
- Claude возвращает coins.json (или zip) с заполненным блоком attribution → ☰ → «Импорт».
- Дома: тот же zip → импорт в scarce_base (скрипт импорта делаем отдельно). Потом ☰ → «Отметить всё как перенесённое».

## Формат coins.json
{ "format":"coinlog", "version":1, "coins":[ { "id":"261106-01", "event":"...", "purchase":{date,price,currency,seller,notes}, "physical":{size_mm,weight_g}, "photos":{obverse,reverse,extra[]}, "attribution":{status none|draft|confirmed, country, issuer, ruler, dates, denomination, metal, mint, refs, sources[], auction_prices, notes}, "transferred":false } ] }
Фото в zip лежат в photos/<имя из coins.json>.

## Важно про данные
Данные хранятся в памяти Chrome на телефоне. Приложение запрашивает защиту от автоочистки, но «Очистить данные сайта» или удаление Chrome их сотрёт. Делай экспорт zip после каждого дня выставки.
