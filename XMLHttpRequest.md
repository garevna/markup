# AJAX

## :mortar_board: `XMLHttpRequest`

###### Спецификация 
```
XMLHttpRequest - это API, 
предоставляющий функциональность на стороне клиента 
для передачи данных между клиентом и сервером 
с помощью скриптов
```
###### :warning: `Same Origin Policy`

`Запрос можно делать только на адреса с тем же протоколом, доменом, портом, что и текущая страница`
###### Конструктор XMLHttpRequest ()
###### Создает экземпляр объекта для обмена данными с сервером:
```javascript
var request = new XMLHttpRequest ()
```
###### Прототипом является **`XMLHttpRequestEventTarget`**, который наследует от **`EventTarget`**
###### Экземпляры `XMLHttpRequest` имеют ряд унаследованных событий, свойств и методов

<a name='table'></a>

| `Методы` | `События` | `Свойства` |
|-|-|-|
| [:arrow_right_hook: `open()`](#mortar_board-open) | ✅ `readystatechange` | [:arrow_right_hook: **`onreadystatechange`**](#mortar_board-onreadystatechange) |
| [:arrow_right_hook: `send()`](#mortar_board-send) | | [:arrow_right_hook: **`readyState`**](#mortar_board-readystate) |
|  | | [:arrow_right_hook: **`status`**](#mortar_board-status) |
|  | | [:arrow_right_hook: `statusText`](#mortar_board-statustext) |
|  | ✅ `loadstart` | [:arrow_right_hook: `onloadstart`](#on) |
|  | ✅ `progress` | [:arrow_right_hook: `onprogress`](#on) |
|  | ✅ `loadend` | [:arrow_right_hook: `loadend`](#on) |
|  | ✅ `load` | [:arrow_right_hook: `onload`](#mortar_board-onload) |
|  | ✅ `error`  | [:arrow_right_hook: `onerror`](#mortar_board-onerror) |
|  | ✅ `timeout` | [:arrow_right_hook: `ontimeout`](#mortar_board-ontimeout)|
| ✅ `abort()` | ✅ `abort` | ✅ `onabort` |
| [:arrow_right_hook: `setRequestHeader()`](#mortar_board-setrequestheader) |  | [:arrow_right_hook: **`responseType`**](#mortar_board-responsetype) |
| :arrow_right_hook: [`getAllResponseHeaders()`](#mortar_board-getallresponseheaders) | | [:arrow_right_hook: **`responseText`**](#mortar_board-responsetext) |
| ✅ `getResponseHeader()` | | ✅ `responseURL` |

Ответ сервера имеет заголовок ответа ( **`header`** ) и тело ответа ( **`response`** )

### :mortar_board: `open`

Метод `open` устанавливает соединение с сервером

Первый аргумент - метод доступа ( строка ), может принимать одно из значений:

    ✅ GET
    ✅ POST
    ✅ PUT
    ✅ DELETE

Второй аргумент - URL ресурса ( файла ), откуда предполагается получить ( **`GET`** ) или куда предполагается записать ( **`POST`**, **`PUT`**, **`DELETE`** ) данные

Третий аргумент ( опциональный, по умолчанию **`true`** ) позволяет сделать запрос синхронным, если установить его значение в `false` ( :warning: чего делать категорически не рекомендуется )

:coffee:
```javascript
var request = new XMLHttpRequest ()
request.open ( 
    'GET', 
    'https://ajax.googleapis.com/ajax/libs/jquery/2.2.0/jquery.min.js'
)
```
***
### :mortar_board: `send()`

Метод send() отправляет тело запроса на сервер

При запросе на получение данных ( **`GET`** ) тело запроса отсутствует

:coffee:
```javascript
var request = new XMLHttpRequest ()
request.open ( 
    'GET', 
    'https://ajax.googleapis.com/ajax/libs/jquery/2.2.0/jquery.min.js'
)
request.send()
```
| [:arrow_double_up:](#table) |
|-|

При передаче данных на сервер ( **`POST`**, **`PUT`**, **`DELETE`** ) структура данных должна соответствовать формату, переданному в заголовке запроса [**`Content-Type`**](#-content-type)

***

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

| [:arrow_double_up:](#table) |
|-|

***
### :mortar_board: `status`

:warning: Только для чтения

Содержит код завершения операции

Если запрошенные данные благополучно загружены, то значением будет  200

В противном случае значением будет код ошибки ( например, 404 )

***
### :mortar_board: `statusText`

:warning: Только для чтения

Текст статуса ответа сервера, соответствующий коду

если `status === 200`,  то  `statusText` будет `"OK"`

если `status === 404`,  то  `statusText` будет `"Not Found"`

| [:arrow_double_up:](#table) | [:link: MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) |
|-|-|

***

### :mortar_board: `responseText`

:warning: Только для чтения

"Тело" ответа сервера

При получении от сервера текстового файла содержимое файла будет значением этого свойства

При обработке асинхронного запроса данные могут быть загружены не полностью, но значение `responseText` всегда содержит 
тот текст, который уже получен от сервера

Свойство `responseText` допустимо только для текстового содержимого

***

| [:arrow_double_up:](#table) |
|-|

### :mortar_board: Обработка событий
Значения свойств, начинающиеся на **`on`**, могут быть ссылкой на колбэк-функцию, которая будет вызвана в момент возникновения события

Тип обрабатываемого события - текст, следующий за **`on`** в имени свойства

#### :mortar_board: `onreadystatechange`

Свойство, значение которого является ссылкой на колбэк-функцию, которая будет обрабатывать событие изменения значения  `readyState`

Назначить обработчика нужно обязательно:
```javascript
var transport = new XMLHttpRequest ()

transport.onreadystatechange = function ( event ) {
   if ( this.readyState === 4 && 
        this.status === 200 ) 
           console.log ( event )
}
```
При вызове колбэк-функции ей будет передан объект события:
```console
▼ Event {isTrusted: true, type: "readystatechange", target: XMLHttpRequest, currentTarget: XMLHttpRequest, eventPhase: 2, …}
    bubbles: false
    cancelBubble: false
    cancelable: false
    composed: false
  ► currentTarget: XMLHttpRequest { onreadystatechange: ƒ, readyState: 4, timeout: 0, withCredentials: false, upload: XMLHttpRequestUpload, … }
    defaultPrevented: false
    eventPhase: 0
    isTrusted: true
  ► path: []
    returnValue: true
  ► srcElement: XMLHttpRequest { onreadystatechange: ƒ, readyState: 4, timeout: 0, withCredentials: false, upload: XMLHttpRequestUpload, … }
  ► target: XMLHttpRequest { onreadystatechange: ƒ, readyState: 4, timeout: 0, withCredentials: false, upload: XMLHttpRequestUpload, … }
    timeStamp: 87810968.4
    type: "readystatechange"
  ► __proto__: Event
```

| [:arrow_double_up:](#table) | [:coffee::one:](https://plnkr.co/edit/b5gXN9q5FdturHenpo3b?p=preview) | [:link: `Errors ( status values )` ](https://www.w3schools.com/tags/ref_httpmessages.asp) |
|-|-|-|

###### Остальные события ( `loadstart`, `loadend`, `progress`, `load`, `error`, `timeout` ) отличаются от события **`readystatechange`** - они относятся к категории **_`ProgressEvent`_**:

```console
▼ ƒ ProgressEvent()
    arguments: null
    caller: null
    length: 1
    name: "ProgressEvent"
  ► prototype: ProgressEvent {constructor: ƒ, Symbol(Symbol.toStringTag): "ProgressEvent"}
  ► __proto__: ƒ Event()
```

#### :mortar_board: `onload`

Это свойство содержит ссылку колбэк-функцию, которая будет обрабатывать событие благополучного завершения загрузки данных с сервера
```javascript
var transport = new XMLHttpRequest ()

transport.onload = function () {
    console.log ( this.responseText )
}
```
<a name="on"></a>
#### :mortar_board: `onloadstart` | `onprogress` | `onloadend`
```javascript
var request = new XMLHttpRequest()
request.open (
    "get",
    'https://httpbin.org/get',
    true 
)
request.responseType = "arraybuffer";

request.onloadstart = function( event ) {
   console.log ( 'START' )
}
request.onloadend = function( event ) {
   console.log ( 'END' )
}
request.onprogress = function( event ) {
   console.log ( `progress: ${event.loaded} / ${event.total}` )
}
request.onload = function( event ) {
   console.log ( this.response )
}
request.send ()
```

| [:arrow_double_up:](#table) |
|-|

#### :mortar_board: `ontimeout`

Это свойство содержит ссылку колбэк-функцию, которая будет вызвана, когда истечет временной интервал, установленный с
```javascript
var request = new XMLHttpRequest()
request.open (
    "POST",
    'https://httpbin.org/post'
)

request.setRequestHeader (
    "Content-Type",
    "application/x-www-form-urlencoded"
)
request.timeout = 100
request.ontimeout = function( event ) {
   console.log ( event )
}
```

#### :mortar_board: `onerror`

Это свойство содержит ссылку колбэк-функцию, которая будет обрабатывать ошибки, возникающие при загрузке данных с сервера
```javascript
var transport = new XMLHttpRequest ()

transport.onerror = function ( err ) {
    console.log ( this.responseText )
}
```
| [:arrow_double_up:](#table) | [:coffee::two:](https://plnkr.co/edit/BqbCvoAnbikBtTFTRBHp?p=preview) | [:coffee::three:](https://plnkr.co/edit/DLH49iWObtxqcijNT9oY?p=preview) |
|-|-|-|

***

### :mortar_board: setRequestHeader()

Метод устанавливает заголовок запроса

* первый аргумент - имя заголовка
* второй аргумент - значение

:warning: вызывается после **`open ()`**, но перед **`send ()`**

#### :memo: [**Заголовки запроса**](https://flaviocopes.com/http-request-headers/)

###### ✅ Content-Type
Этот заголовок определяет тип пересылаемого контента

**`"Content-Type"  :  "тип  /  подтип  [ ; параметр ]"`**

`Тип используется для объявления общего типа данных, а подтип определяет специальный формат для данных этого типа`

Типы:

        ✅ application
        ✅ audio
        ✅ image
        ✅ message
        ✅ multipart
        ✅ text
        ✅ video

**`multipart`**  `- содержимое состоит из нескольких частей, включающих данные различных типов`

:warning: `Для незарегестрированного типа содежимого имя должно начинаться с "X-"`

:clipboard: `Примеры возможных значений `**`Content-Type:`**

        ✏️ application/msword
        ✏️ application/pdf
        ✏️ image/gif
        ✏️ image/jpeg
        ✏️ image/png
        ✏️ text/html
        ✏️ text/plain
        ✏️ video/mpeg
        ✏️ text/html; charset=utf-8
        ✏️ multipart/form-data
        ✏️ multipart/mixed; boundary="____________________"

`( в последнем примере строка "____________________" указывается как разделитель для различных фрагментов контента`

`В начале каждого фрагмента может быть задана своя строка с полем "Content-Type" )`

`boundary ( граница ) — это последовательность байтов, которая не должна встречаться внутри пересылаемого контента`

| [:arrow_double_up:](#table) | [:coffee: Упражнения](setRequestHeader-samples) |
|-|-|

Политика безопасности ограничивает доступ к некоторым заголовкам ( например, `Origin` )

#### CSRF

**Сross Site Request Forgery** ( межсайтовая подделка запроса )

Когда юзер заходит на сайт, созданный злоумышленником, от его лица может быть отправлен запрос на другой сервер, на котором юзер аутентифицирован

CSRF-атака возможна только в том случае, если сервер не требует обязательного включения в запрос подтверждения  со стороны юзера, которое не может подделано атакующим скриптом

Для защиты от CSRF-атак можно использовать заголовок

        X-CSRF-TOKEN

* Токен должен быть предоставлен сервером
* Его можно записать в куки на клиенте
* При отправке запроса можно добавить заголовок X-CSRF-TOKEN со значением токена, предоставленным сервером

`При получении ( POST - PUT - DELETE ) запроса сервер проверяет заголовок  X-CSRF-TOKEN, и если значение не совпадает с токеном клиента или заголовок отсутствует, запрос отклоняется`

```javascript
var xhr = new XMLHttpRequest()
xhr.open (
    "POST",
    'http://ptsv2.com/t/garevna/post', true
)

xhr.setRequestHeader (
    "Content-Type",
    "application/x-www-form-urlencoded"
)
xhr.setRequestHeader(
    "X-CSRF-TOKEN",
    "AIJu7NUduZPGo-7uZ"
)

xhr.onreadystatechange = function() {
    if( this.readyState === 4 && this.status === 200 ) {
         console.log ( 'success' )
         console.log ( this.responseText )
    }
}
xhr.send ( "name=garevna&speciality=frontEnd" )
```

| [:arrow_double_up:](#table) |
|-|

### :mortar_board: `responseType`

Свойство **`responseType`** объекта `XMLHttpRequest` определяет тип данных ответа сервера

Возможными значениями являются:

* пустая строка (по умолчанию)
* arraybuffer
* blob
* document
* json
* text

Свойство **`response`** будет содержать тело объекта в соответствии с `responseType`

* ArrayBuffer
* Blob
* Document
* JSON
* string

Если запрос завершился неудачей, то значением **`response`** будет `null`

:coffee:
###### Получение двоичных данных
```javascript
var request = new XMLHttpRequest()
request.open (
    "get",
    'https://httpbin.org/get'
)
request.responseType = "arraybuffer"

request.onreadystatechange = function() {
   if (
      this.readyState === 4
      && this.status === 200 
   ) {
        console.log ( this.response )
   }
}
request.send ()
```
***
| [:arrow_double_up:](#table) |
|-|

### :mortar_board: getAllResponseHeaders()

```javascript
var transport = new XMLHttpRequest ()

transport.onload = function ( event ) {
    console.dir ( this.getAllResponseHeaders() )
}
transport.open ( 
    'GET', 
    'https://ajax.googleapis.com/ajax/libs/jquery/2.2.0/jquery.min.js'
)
transport.send()
```
Заголовки ответа сервера:
```console
last-modified: Tue, 20 Dec 2016 18:17:03 GMT
content-type: text/javascript; charset=UTF-8
cache-control: public, max-age=31536000, stale-while-revalidate=2592000
expires: Wed, 09 Oct 2019 00:23:02 GMT
```

| [:arrow_double_up:](#table) | [💼 Упражнения](https://docs.google.com/forms/d/e/1FAIpQLSdA3JwhlOTXdZxCO3y1MdLe-pe-cynNVGeboy7IV0aWHliGHA/viewform)
|-|

***
[Протокол TCP](https://xakep.ru/2002/04/11/14943/)
[RFC793](https://www.lissyara.su/doc/rfc/rfc793/)
