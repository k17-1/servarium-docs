- [Central server API](central_server.md)
- [Local server API](local_server.md)

# Центральный сервер
Два ендпоинта: для локальных серверов и для клиентов.

Для локальных серверов: `/localserver/`

Для клиентов: `/api/`

Далее добавляется версия: `/v1/`

Для локальных серверов необходимо вставлять header `Authorization: bearer token`. Токен берется при создании сабсервера.


# Локальный сервер:
TODO

# Формат ответа
Ответ в случае успешного выполнения запроса:
```json
{
  "ok": true,
  "data": {}
}
```
Ответ в случае ошибки:
```json
{
  "ok": false,
  "err": ERR_NUMBER,
  "reason": DESC
}
```
где `ERR_NUMBER` - код ошибки, `DESC` - краткое описание.
