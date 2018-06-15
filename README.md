# **TalkMachine**

## Содержание

* Ошибки и сообщения
    * Атомарное сообщение
    * Классификация кодов сообщений
    * Ошибки форм

* API

## Ошибки и сообщения

### Атомарное сообщение
Все сообщения и ошибки ошибки в конечном счете состоят из комбинации (или только из самой одной) атомарных ошибок. Атомарная ошибка характеризуется двумя параметрами: **кодом** и **текстом**.

```javascript
// atomic message object (AEO)
{
    'c': 1234, // 'c' - Код. Всего одна буква, т.к. таких сообщений очень много, поэтому есть смысл сэкономить объем
    't': 'Error text' // 't' - Текст.
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

### Ошибки форм

```javascript
{
    'global': [
        'List of', 
        'global (multifield)', 
        'errors for this form'
    ],
    'fields': [
        'fieldname': [
            'list of errors for this field'
        ],
        // ...
        'last_field': [
            
        ]
    ]
}
```

## API

### **POST Login**

URL: `/user/login`

REQUEST

```javascript
{
    'email': 'example@example.com',
    'password': 'qwerty123'
}
```

RESPONSE 200

```javascript
// Detailed own info

{
    'nickname': 'Nagibator',
    'name': 'Lev Tolstoy'
    'email': 'lev.tolstoy@ya.ru'
    'avatar': '/avatar/url' // url аватара
    'bio': 'A Russian writer who is regarded as one of the greatest authors of all time'
}
```
RESPONCE 401

```
{
    
}
```

