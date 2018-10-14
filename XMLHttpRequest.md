# AJAX

## :mortar_board: `XMLHttpRequest`

Это конструктор
С его помощью создается объект для обмена данными с сервером:
```javascript
var request = new XMLHttpRequest ()
```
Экземпляр объекта, созданного с помощью конструктора `XMLHttpRequest`, имеет ряд унаследованных событий, свойств и методов

| Методы | События | Свойства |
|-|-|-|
| ✅ `open()` | ✅ `readystatechange` | ✅ `onreadystatechange` |
| ✅ `setRequestHeader()` | ✅ `load` | ✅ `response` |
| ✅ `send()` | ✅ `error`  | ✅ **`responseText`** |
| | | ✅ `responseType` |
| | | ✅ `responseURL` |
| | | ✅ **`status`** |
| | | ✅ `statusText` |
| | | ✅ **`readyState`** |

Ответ сервера имеет заголовок ответа ( **`header`** ) и тело ответа ( **`responseText`** )

>> :warning: `Ограничение   "Same Origin Policy"`

>> `Суть - "каждый сайт в своей песочнице"`

>> `Запрос можно делать только на адреса с тем же протоколом, доменом, портом, что и текущая страница`

### :mortar_board: `open`

Метод `open` устанавливает соединение с сервером

Первый аргумент - метод ( строка ), может принимать одно из значений:

    ✅ GET
    ✅ POST
    ✅ PUT
    ✅ DELETE
```javascript
var request = new XMLHttpRequest ()
request.open ( 
    'GET', 
    'https://ajax.googleapis.com/ajax/libs/jquery/2.2.0/jquery.min.js'
)
```

### :mortar_board: `readyState`

:warning: Только для чтения

`Содержит инфо о стадии прохождения запроса`

| | Запрос проходит стадии: |
|-|-|
| 0 | `запрос создан, но метод open () еще не был вызван` |
| 1 | `метод open () был вызван; можно формировать заголовки запроса` |
| 2 | `метод send() был вызван, и заголовки ответа сервера получены ( можно читать status )` |
| 3 | `идет процесс загрузки тела ответа сервера` |
| 4 | `процесс загрузки ответа завершен` |

### :mortar_board: `status`

:warning: Только для чтения

Содержит код завершения операции

Если запрошенные данные благополучно загружены, то значением будет  200

В противном случае значением будет код ошибки ( например, 404 )

### :mortar_board: `statusText`

:warning: Только для чтения

Текст статуса ответа сервера, соответствующий коду

если `status === 200`,  то  `statusText` будет `"OK"`

если `status === 404`,  то  `statusText` будет `"Not Found"`

### :mortar_board: `responseText`

:warning: Только для чтения

"Тело" ответа сервера

При получении от сервера текстового файла содержимое файла будет значением этого свойства

При обработке асинхронного запроса данные могут быть загружены не полностью, но значение `responseText` всегда содержит 
тот текст, который уже получен от сервера

Свойство `responseText` допустимо только для текстового содержимого

### :mortar_board: `onreadystatechange`

Свойство, значение которого является ссылкой на колбэк-функцию, которая будет обрабатывать событие изменения значения  `readyState`

Назначить обработчика нужно обязательно:
```javascript
var transport = new XMLHttpRequest ()

transport.onreadystatechange = function () {
   if ( this.readyState === 4 && 
        this.status === 200 ) 
           console.log ( this.responseText )
}
```
Функция-колбэк должна проверять значение `readyState`, и если это значение равно 4, то можно проверить значение свойства `status`

Если `status === 200`, то можно получить ответ, который будет в свойстве `responseText` ( если мы имеем дело с текстовыми данными )

|[:coffee::one:](https://plnkr.co/edit/b5gXN9q5FdturHenpo3b?p=preview)|[:link: `Errors ( status values )` ](https://www.w3schools.com/tags/ref_httpmessages.asp)
|-|-|

### :mortar_board: `onload`

Это свойство содержит ссылку колбэк-функцию, которая будет обрабатывать событие благополучного завершения загрузки данных с сервера
```javascript
var transport = new XMLHttpRequest ()

transport.onload = function () {
    console.log ( this.responseText )
}
```

### :mortar_board: `onerror`

Это свойство содержит ссылку колбэк-функцию, которая будет обрабатывать ошибки, возникающие при загрузке данных с сервера
```javascript
var transport = new XMLHttpRequest ()

transport.onerror = function ( err ) {
    console.log ( this.responseText )
}
```
| [:coffee::two:](https://plnkr.co/edit/BqbCvoAnbikBtTFTRBHp?p=preview) | [:coffee::three:](https://plnkr.co/edit/DLH49iWObtxqcijNT9oY?p=preview) |
|-|-|