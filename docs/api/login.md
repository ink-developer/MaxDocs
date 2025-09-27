# Вход по номеру телефона

## 1. Запрос кода

### Opcode: `17`

#### Пример запроса

```json
{
    "ver": 11,
    "cmd": 0,
    "seq": 1,
    "opcode": 17,
    "payload": {
        "phone": "+7111111111",
        "type": "START_AUTH",
        "language": "ru"
    }
}
```

#### Параметры запроса

| Аргумент   | Тип  | Обязательный | Описание                                         |
|:------------|:------:|:--------------:|:-------------------------------------------------|
| `phone`      | str  | ✅           | Номер телефона в формате E.164 (+7XXXXXXXXXX)  |
| `type`       | str  | ✅           | Статическая строка "START_AUTH"                |
| `language`   | str  | ✅           | Язык в формате ISO 639-1 (ru, en и т.д.)      |

#### Ответ

```json
{
  "ver": 11,
  "cmd": 1,
  "seq": 1,
  "opcode": 17,
  "payload": {
    "requestMaxDuration": 60000,
    "requestCountLeft": 10,
    "altActionDuration": 60000,
    "codeLength": 6,
    "token": "An_Sx...."
  }
}
```
#### Параметры ответа


| Аргумент              | Тип  | Описание                                                                 |
|:-----------------------|:------:|:-------------------------------------------------------------------------|
| `requestMaxDuration`    | int  | Максимальное время действия запроса в мс (обычно 60000)                 |
| `requestCountLeft`      | int  | Остаток попыток запроса кода (обычно 10)                                |
| `altActionDuration`     | int  | Время действия альтернативного действия в мс (обычно 60000)             |
| `codeLength`            | int  | Длина кода подтверждения (обычно 6)                                     |
| `token`                 | str  | Промежуточный токен для последующей проверки кода                       |

---

## 2. Отправка кода

### Opcode - `18`

#### Пример запроса

```json
{
  "ver": 11,
  "cmd": 0,
  "seq": 5,
  "opcode": 18,
  "payload": {
    "token": "An_Sx...",
    "verifyCode": "XXXXXX",
    "authTokenType": "CHECK_CODE"
  }
}
```

#### Параметры запроса

| Аргумент        | Тип  | Обязательный | Описание                                         |
|:-----------------|:------:|:--------------:|:-------------------------------------------------|
| `token`           | str  | ✅           | Токен, полученный при запросе кода              |
| `verifyCode`      | str  | ✅           | Код подтверждения, полученный по SMS           |
| `authTokenType`   | str  | ✅           | Статическая строка "CHECK_CODE"                |

#### Ответ

```json
{
  "ver": 11,
  "cmd": 1,
  "seq": 5,
  "opcode": 18,
  "payload": {
    "tokenAttrs": {
      "LOGIN": {
        "token": "An_Sx..."
      }
    },
    "profile": {
      "profileOptions": [],
      "contact": {
        "accountStatus": 0,
        "names": [
          {
            "name": "Ink",
            "firstName": "Ink",
            "lastName": "",
            "type": "ONEME"
          }
        ],
        "phone": 71111111111,
        "options": [
          "TT",
          "ONEME"
        ],
        "updateTime": 1755072926792,
        "id": 11111111
      }
    }
  }
}
```


#### Параметры ответа

| Аргумент                     | Тип   | Описание                                                                 |
|:-------------------------------|:-------:|:-------------------------------------------------------------------------|
| `tokenAttrs`                    | obj   | Содержит токены, полученные после подтверждения кода                    |
| `tokenAttrs.LOGIN.token`         | str   | Токен для дальнейшей аутентификации                                     |
| `profile`                        | obj   | Профиль пользователя                                                    |
| `profile.contact`                | obj   | Контактная информация пользователя                                       |
| `profile.contact.accountStatus`  | int   | Статус аккаунта (0 — активен)                                           |
| `profile.contact.names`          | list  | Список имен пользователя                                                |
| `profile.contact.names[].name`   | str   | Полное имя пользователя                                                 |
| `profile.contact.names[].firstName` | str | Имя пользователя                                                      |
| `profile.contact.names[].lastName`  | str | Фамилия пользователя                                                  |
| `profile.contact.names[].type`      | str | Тип имени (например, "ONEME")                                         |
| `profile.contact.phone`          | int   | Номер телефона пользователя без "+"                                     |
| `profile.contact.options`        | list  | Дополнительные опции пользователя                                       |
| `profile.contact.updateTime`     | int   | Время последнего обновления профиля (ms)                                |
| `profile.contact.id`             | int   | Уникальный идентификатор контакта                                       |
