# API Aroshka Cloud: полная документация

> **Фрилансерам:** прежде чем браться за заказы, связанные с этим сервисом, прочитайте [предупреждение](WARNING_FOR_FREELANCERS.md) о ситуации, с которой мы столкнулись на бирже Kwork.

Документация API облачного хранилища [aroshka.cloud](https://aroshka.cloud). Сохранена 22.10.2026 из личного
кабинета (тариф с доступом к API), потому что сама Aroshka выдаёт её только онлайн владельцу аккаунта
и скачать не даёт.

| Файл | Что внутри |
|---|---|
| `openapi.json` | Исходная спецификация OpenAPI 3.1 целиком, ровно та, из которой строится страница aroshka.cloud/api-docs. 36 путей, 46 методов, все схемы ответов. Открывается в Swagger Editor, Redoc, Postman, Insomnia |
| `ENDPOINTS.md` | Справочник по всем 46 методам на русском: путь, параметры, поля тела запроса, коды ответов. Собран из `openapi.json` |

## Главное для работы

- База API: `https://aroshka.cloud/api/v1`
- Авторизация: заголовок `Authorization: Bearer <ключ>`, плюс `Accept: application/json`.
- Ключ создаётся в кабинете: Настройки, Разработчик, API-ключи. Показывается один раз.
- Формат ключа: `номер|строка`, например `123|abc...`. Копировать нужно целиком, вместе с номером и вертикальной
  чертой. Без номера API отвечает `401 {"message":"Unauthenticated."}` (проверено 22.10.2026).
- Разделы: Files 14, Workspaces 13, File requests 8, Links 4, Tags 4, Sharing 3.

## Список файлов и папок

`GET /drive/file-entries` - главный метод для выгрузки. Параметр `section` обязателен (без него ответ 422
«Поле section обязательно для заполнения»). Остальные: `folder_id`, `type`, `owner` (me / not_me), `location`
(trashed / starred), `sharing`, `query`, `per_page`, `page`, `sort`, `created_at`, `updated_at`.
Ответ постраничный: `data` (массив DriveEntry), `links`, `meta`, `folder`.

```bash
curl -H "Authorization: Bearer $AROSHKA_KEY" -H "Accept: application/json" \
  "https://aroshka.cloud/api/v1/drive/file-entries?section=home&per_page=50&page=1"
```

Обход всех папок: берём записи с `type=folder` и запрашиваем их содержимое через `folder_id`, пока
`links.next` не пустой.

## Как посмотреть документацию удобно

Открыть https://editor.swagger.io и через File, Import file загрузить `openapi.json`, или в Postman: Import,
выбрать файл. Ключи и куки в этом репозитории не хранятся.
