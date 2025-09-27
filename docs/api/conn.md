# Подключение

### Opcode — 6


#### Пример запроса


```json
{
  "ver": 11,
  "cmd": 0,
  "seq": 0,
  "opcode": 6,
  "payload": {
    "userAgent": {
      "deviceType": "WEB",
      "locale": "ru",
      "deviceLocale": "ru",
      "osVersion": "Linux",
      "deviceName": "Chrome",
      "headerUserAgent": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/139.0.0.0 Safari/537.36",
      "appVersion": "25.8.5",
      "screen": "1080x1920 1.0x",
      "timezone": "Europe/Moscow"
    },
    "deviceId": "893bef87-6eb6-4b90-80d0-0a304e2dbf74"
  }
}
```

#### Параметры запроса

| Аргумент          | Тип    | Обязательный | Описание                                                                 |
|:------------------|:--------:|:--------------:|:-------------------------------------------------------------------------|
| `deviceType`        | str    | ✅           | Тип устройства: WEB, Android, iOS                                        |
| `locale`            | str    | ✅           | Язык интерфейса в формате ISO 639-1                                      |
| `deviceLocale`      | str    | ✅           | Язык устройства в формате ISO 639-1                                       |
| `osVersion`         | str    | ✅           | Версия операционной системы                                               |
| `deviceName`        | str    | ✅           | Имя устройства или браузера                                               |
| `headerUserAgent`   | str    | ✅           | User-Agent браузера или приложения                                        |
| `appVersion`        | str    | ✅           | Версия приложения                                                        |
| `screen`            | str    | ✅           | Разрешение экрана и масштаб, например 1080x1920 1.0x                      |
| `timezone`          | str    | ✅           | Часовой пояс в формате IANA                                              |
| `deviceId`          | str    | ✅           | Уникальный идентификатор устройства (UUID v4)                             |

#### Ответ

```json
{
  "ver": 11,
  "cmd": 1,
  "seq": 0,
  "opcode": 6,
  "payload": {
    "location": "DE",
    "app-update-type": null
  }
}
```

#### Параметры ответа

| Аргумент         | Тип  | Описание                                         |
|:-----------------|:------:|:-------------------------------------------------|
| `location`        | str  | Код страны в ISO 3166-1 alpha-2                |
| `app-update-type` | any  | Тип обновления приложения (если доступно)      |
