# **TalkMachine**

## Содержание

* Ошибки и сообщения
    * Атомарное сообщение
    * Классификация кодов сообщений
    * Ошибки форм

* API

## Ошибки и сообщения

### Атомарное сообщение
Все сообщения и ошибки ошибки в конечном счете состоят из комбинации (или только из самой одной) атомарных ошибок. Атомарная ошибка характеризуется тремя параметрами: **кодом**,  **текстом** и **данными**.

```javascript
// atomic message object (AEO)
{
    'c': 1234, // 'c' - Code - код сообщения. Всего одна буква, т.к. таких сообщений очень много, поэтому есть смысл сэкономить объем
    't': 'Message text' // 't' - Text - текст сообщения.
    'd': 'tolstoy@lev.ru' // 'd' - Data (Данные). Опционально, если, например, это поле заполнено корректно и нам нужно сохранить его значение
}
```

### Классификация кодов сообщений

// TODO:

Здесь пока ничего нет, но идея такова: сообщения AJAX будут в одном диапазоне значений, а сообщения Websocket в другом диапазоне.

Также в кажом диапазоне есть поддиапазоны для информационных сообщений, сообщений об ошибке и (возможно) сообщений об успешном заверешнии

Пример:

```
[-------------- AJAX -------------][----------- Websocket -----------]
 [-- suc --][-- log --][-- err --]  [-- suc --][-- log --][-- err --]
```

Код до 2х байт:

Маска
```
[ , ] [ , ] [ , , , ] [ , , , , , , , ]
 код   рез.   тема         подтема
```
* Код
    * 00 - AJAX
    * 01 - WS
* Рез. (результат) _использование всех кодов, конечно, под вопросом) но пусть лучше будет_
    * 00 - Success
    * 01 - Info
    * 10 - Error
    * 11 - Warning

### Ошибки форм

```javascript
{
    // ошибки формы в целом
    'global': [
        {}, {}, {} // list of AEO
    ],
    // ошбики к каждому полю конкретно
    'fields': [
        'fieldname': [
            {}, {}, {} // list of AEO
        ],
        // ...
        'last_field': [
            {}, {}, {} // list of AEO
        ]
    ]
}
```

### Сообщения

**Ошибки**

```javascript
// incorrect email format
{
    'c': 000, // TODO:
    't': 'Incorrect email format'
}
```

```javascript
// Email already in use
{
    'c': 000, // TODO:
    't': 'Email already in use'
}
```

```javascript
// Nickname already in use
{
    'c': 000, // TODO:
    't': 'Nickname already in use'
}
```


```javascript
// Incorrect password length
{
    'c': 000, // TODO:
    't': 'Minimum length 8 characters'
}
```

```javascript
// Passwords do not match
{
    'c': 000, // TODO:
    't': 'Passwords do not match'
}
```

```javascript
// Incorrect email or password
{
    'c': 000, // TODO:
    't': 'Incorrect email or password'
}
```

```javascript
// Required field
{
    'c': // TODO:
    't': 'Required field'
}
```

```javascript
// Logout error
{
    'c': 000, // TOOD:
    't': 'Can not log out'
}
```



## API

### **GET Me**

URL `/user/me`

RESPONCE 200
```javascript
{
    'nickname': 'Nagibator',
    'name': 'Lev Tolstoy'
    'email': 'lev.tolstoy@ya.ru'
    'avatar': '/avatar/url' // url аватара
    'bio': 'A Russian writer who is regarded as one of the greatest authors of all time'
}
```

### **POST Login**

**URL** `/user/login`

**REQUEST**

```javascript
{
    'email': 'example@example.com',
    'password': 'qwerty123'
}
```

**RESPONCE** 200 - аналогично `/user/me`

**RESPONCE  with errors**

Ошибки согласно формату ошибки форм и сообщениям согласно задекларированнм

### **POST Register**

**URL** `/user/register`

**REQUEST**

```javascript
{
    'email': 'lev.tolstoy@ya.ru',
    'nickname': 'Lyova',
    'password': 'qwerty123'
}
```

**RESPONCE** 200 - аналогично `/user/me`

**RESPONCE with errors**

Ошибки согласно формату ошибки форм и сообщениям согласно задекларированнм

### **POST Logout**

**URL** `/user/logout`

**RESPONCE 200**

```javascript
{
    'c': 000, // TODO:
    't': 'Logged out successfully'
}
```

RESPONCE 400

```javascript
{
    'c': 000, // TOOD:
    't': 'Can not log out'
}
```

**RESPONCE with errors**

Ошибки согласно формату ошибки форм и сообщениям согласно задекларированнм

