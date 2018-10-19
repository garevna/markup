# :mortar_board: Fetch API

Интерфейсы Fetch API 

| [:arrow_right_hook: Request](#mortar_board-request) | [:arrow_right_hook: Response](#mortar_board-response) |
|-|-|

Метод **`fetch`** объекта `window` реализует только асинхронные AJAX-запросы

Метод **`fetch`** возвращает **_промис_**

Обязательный первый аргумент метода **`fetch`** - это url ресурса
```javascript
fetch ( "message.txt" )
    .then ( response => {
        ...
    })
```
Когда промис завершится, он вернет объект [**`Response`**](#mortar_board-response)

## :mortar_board: Request

Свойство **`prototype`** конструктора **`Request`**:

| Свойства | Методы |
|-|-|
| bodyUsed | arrayBuffer() |
| cache | blob() |
| [credentials](#credentials) | clone() |
| destination | formData() |
| [headers](#headers) | json() |
| integrity | text() |
| isHistoryNavigation |  |
| keepalive |  |
| [:information_source: method](#method) |  |
| [:information_source: mode](#mode) |  |
| redirect |  |
| referrer |  |
| referrerPolicy |  |
| signal |  |
| [:information_source: url](#url) |  |

### :information_source: method

| [:arrow_heading_up:](#mortar_board-request) | `GET` | `POST` | `PUT` | `DELETE` | `HEAD` |
|-|-|-|-|-|-|

```javascript
var request = new Request( 
    'https://httpbin.org/post', 
    {
        method: 'GET'
    }
)
```

### :information_source: mode

`Режим запроса`

| [:arrow_heading_up:](#mortar_board-request) | [`cors`](#cors) | [`no-cors`](#no-cors) | `same-origin` | `navigate` |
|-|-|-|-|-|

###### `same-origin`

Запросы из других источников будут приводить к генерации исключения

:coffee: Например, запрос
```javascript
var request = new Request( 
    'https://avatars2.githubusercontent.com/u/46?v=4',
    {
        mode: 'same-origin'
    }
)
fetch ( request )
    .then ( response => {
        console.log ( response )
    })
```
приведет к генерации исключения:
```console
Fetch API cannot load https://avatars2.githubusercontent.com/u/46?v=4
Request mode is "same-origin" 
but the URL's origin is not same as the request origin null
```
в результате чего промис завершится неудачей:
```console
Promise {<rejected>: TypeError: Failed to fetch
```

###### `no-cors`

| [:arrow_heading_up:](#information_source-mode) |
|-|

В таком режиме при кросс-доменном запросе исключение не будет сгенерировано, но ответ будет пустым
```javascript
var request = new Request( 
    'https://avatars2.githubusercontent.com/u/46?v=4',
    {
        mode: 'no-cors'
    }
)

fetch ( request )
    .then ( response => {
        response.blob().then ( response => {
            console.log ( response )
        })
    })
```
На такой запрос ответ будет:

```console
Blob(0) { size: 0, type: "" }
```
Если тот же запрос сделать без
```javascript
mode: 'no-cors'
```
то ответ будет:
```console
Blob(35635) { size: 35635, type: "image/jpeg" }
```

###### `cors`

| [:arrow_heading_up:](#information_source-mode) |
|-|

Разрешает кросс-доменные запросы ( :warning: если домен, куда направляется запрос, поддерживает CORS )

:coffee: Например, запрос:
```javascript
var request = new Request( 
    'http://bm.img.com.ua/img/prikol/images/large/0/0/307600.jpg',
    {
        mode: 'cors'
    }
)
fetch ( request )
    .then ( response => {
        console.log ( response )
    })
```
приведет к генерации исключения:
```console
Failed to load http://bm.img.com.ua/img/prikol/images/large/0/0/307600.jpg: 
No 'Access-Control-Allow-Origin' header is present on the requested resource
Origin 'null' is therefore not allowed access
If an opaque response serves your needs, 
set the request's mode to 'no-cors' to fetch the resource with CORS disabled
```
и соответствующему "провалу" запроса
```console
Uncaught (in promise) TypeError: Failed to fetch
```
Это происходит потому, что в режиме **`cors`** требуется, чтобы сервер запрошенного ресурса вернул заголовок **`Access-Control-Allow-Origin`** со значением, совпадающим со значением **`Origin`** запроса ( а заголовок **`Origin`** нельзя подделать, он устанавливается браузером при отправке запроса на сервер )

:coffee: Если сервер запрошенного ресурса вернет заголовок **`Access-Control-Allow-Origin`** со значением **`*`**, то запрос будет выполнен нормально
```javascript
var request = new Request( 
    'https://httpbin.org/get',
    {
        mode: 'cors'
    }
)
fetch ( request )
    .then ( response => {
        response.text().then ( response => {
            console.log ( response )
        })
    })
```
```console
{
  "args": {}, 
  "headers": {
    "Accept": "*/*", 
    "Accept-Encoding": "gzip, deflate, br", 
    "Accept-Language": "en-US,en;q=0.9,ru;q=0.8", 
    "Connection": "close", 
    "Host": "httpbin.org", 
    "Origin": "null", 
    "Save-Data": "on", 
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36"
  }, 
  "origin": "185.38.217.69", 
  "url": "https://httpbin.org/get"
}
```

**_Cross-Origin Resource Sharing_** ( **CORS** ) - это механизм, который использует дополнительные заголовки HTTP, чтобы сообщить браузеру, что веб-приложение, работающее в одном домене, имеет разрешение на доступ к выбранным ресурсам другого домена

По соображениям безопасности браузеры ограничивают кросс-доменные запросы, инициированные из сценариев

XMLHttpRequest и Fetch API следуют политике одинакового происхождения

Это означает, что веб-приложение, использующее эти API, может запрашивать только ресурсы из того же источника, из которого было загружено приложение ( если только ответ от другого источника не содержит правильные заголовки CORS )

Когда объект запроса создается с помощью конструктора **`Request`**, значение свойства `mode` для этого запроса устанавливается в _`cors`_

```javascript
var request = new Request (
   'http://bm.img.com.ua/img/prikol/images/large/0/0/307600.jpg'
)
console.log ( request.mode ) // cors
```
В противном случае в качестве режима обычно используется **`no-cors`**

например, когда запрос инициируется из разметки, и атрибут `crossorigin` отсутствует 
( для элементов `<link>`, `<script>`, `<img>`, `<audio>`, `<video>`, `<object>`, `<embed>` или `<iframe>` запрос выполняется в режиме **`no-cors`** )

| [:arrow_heading_up:](#information_source-mode) |
|-|

###### url
`url  запрошенного ресурса`

###### headers
`заголовки запроса`

###### referrer
`источник запроса`

###### credentials
`должны ли файлы cookie отправляться с запросом`

| `omit` | `same-origin` | `follow` | `include` |
|-|-|-|-|

```javascript
fetch( 'https://httpbin.org/post', {
    credentials: 'include'  
})
```
###### redirect

| `error` | `manual` |
|-|-|

###### integrity
`дайджест ресурса`

###### cache
`режим кэширования`

| `default` | `reload` | ` no-cache` |
|-|-|-|

### :mortar_board: Заголовки запроса

Объект заголовка запроса можно создать с помощью конструктора:
```javascript
var headers = new Headers ()
```
У этого объекта будет унаследованный метод **`append ()`**, который добавляет новое значение в заголовок:
```javascript
headers.append ( 'Content-Type', 'text/plain' )
headers.append ( 'Custom-Header', 'CustomValue' )
```
###### Другие методы:
* **`delete ()`** удаляет значение из заголовка
* **`get ()`** возвращает указанное значение заголовка
* **`set ()`** устанавливает  значение заголовка
* **`has ()`** проверяет, есть ли такое свойство в объекте headers, и возвращает логическое значение

:coffee: :one:
```javascript
fetch ( url )
    .then ( response => {
        console.log ( response.headers.has ( 'Content-Type' ) )
        console.log ( 'Content-Type: ', response.headers.get ( 'Content-Type' ) )
    }
```

## :mortar_board: Response

###### body
Это объект _ReadableStream_, доступ к которому обеспечивают такие методы объекта **_`Response`_**, как  
**`arrayBuffer()`**,  **`blob()`**,  **`formData()`**,  **`json()`**  или   **`text()`**

Эти методы возвращают ответ сервера в заданном формате

| Методы | возвращают **_промис_**, результатом которого будет |
|-|-|
| [**`arrayBuffer()`**](#arrayBuffer()) | `ArrayBuffer ( строка из нулей и единиц )`
| [**`blob()`**](#blob()) | `объект Blob ( данные в двоичном формате )` |
| [**`clone()`**](#clone()) | `копию объекта Response` |
| [**`formData()`**](#formData()) | `данные FormData` |
| [**`json()`**](#json()) | `данные в JSON-формате` |
| [**`text()`**](#text()) | `данные в текстовом формате` |

###### json()

:coffee: Воспользуемся [**сервисом**](https://api.2ip.ua) для получения полной информации о пользователе ( в данном случае - о самом себе )

Для получения такой инфо методу  **`fetch`**  нужно передать в качестве аргумента строку
```
https://api.2ip.ua/geo.json?ip=
```
Метод  **`fetch`**  вернет промис, поэтому "повесим" обработчика успешного завершения  **`then`**

Как мы знаем, метод  **`then`**  принимает один аргумент - функцию, которая будет вызвана в случае успешного завершения асинхронной операции:
```javascript
fetch ( 'https://api.2ip.ua/geo.json?ip=' )
    .then ( response => {
        ...
    })
```
Эта функция получит в качестве аргумента ответ сервера  **_response_** ( так мы назвали эту переменную )

Нам не нужен весь объект  **_response_**, который вернет нам метод  **`fetch`**

Нам нужен результат ( данные ) в формате  _json_

Используем метод   **`json()`** объекта  **`Response`** 

Мы знаем, что этот метод также вернет промис, т.е. нам нужно еще одного обработчика **`then`**:
```javascript
fetch ( 'https://api.2ip.ua/geo.json?ip=' )
    .then ( response => {
        response.json().then ( response => 
            ...
        )
    })
```
Осталось добавить код, который будет выполнен при успешном завершении второго промиса

Функция, которую мы передали в качестве аргумента второму **`then`**, получит на входе объект данных, являющийся результатом парсинга json-строки

| [:arrow_heading_up:](#mortar_board-response) |
|-|

###### blob()

Давайте посмотрим, что такое объект Blob

Создадим элемент img на странице:
```javascript
var picture = document.createElement ( 'img' )
document.body.appendChild ( picture )
```
Теперь загрузим с помощью fetch изображение из сети ( например, аватар пользователя github ) и итерпретируем ответ сервера как объект Blob:

```javascript
fetch ( 'https://avatars2.githubusercontent.com/u/46?v=4' )
    .then ( response => {
        response.blob().then ( response => {
    	    urlObject = URL.createObjectURL( response)
    	    picture.src = urlObject
        })
    })
```
Если вывести полученный объект в консоль, то мы увидим:
```
► Blob(35635) { size: 35635, type: "image/jpeg" }
```
Изображение получено нами в виде объекта **`Blob`**, и теперь оно является локальным объектом, который нам нужно отобразить на странице в нашем элементе  **_img_**

Поскольку на странице могут отображаться только объекты ( ресурсы ), размещенные в сети и имеющие URL, основная задача - создать такой URL для объекта, уже находящегося в нашем распоряжении и являющимся локальным объектом текущей страницы

Для этого существует метод [**URL.createObjectURL**](createObjectURL)

| [:arrow_heading_up:](#mortar_board-response) |
|-|

###### arrayBuffer()

Этот формат ответа сервера представляет собой строку из нулей и единиц

Объект ArrayBuffer не фрагментирует данные, не выделяет отдельные байты или другие кластеры

Для этого у объекта  ArrayBuffer  есть конструкторы:

✅ Int8Array

Для представления данных в виде последовательности байт

✅ Uint8Array

Для представления данных в виде последовательности шестнадцатибитных значений ( чисел )

Результатом работы конструкторов будет итерабельный объект
```javascript
fetch ( 'https://avatars2.githubusercontent.com/u/46?v=4' )
    .then ( response => {
        response.arrayBuffer().then ( response => {
            console.log ( response )
            console.log ( new Int8Array( response ) )
            console.log ( new Uint8Array( response ) )
        })
    })
```

| [:arrow_heading_up:](#mortar_board-response) |
|-|

###### arrayBuffer --> blob

Можно получить  объект **`Blob`**  из объекта **`arrayBuffer`** с помощью конструктора  **`Blob`**, которому нужно передать объект **`arrayBuffer`**, "завернутый" в массив

:coffee: :one: Закиньте в консоль следующий код, и посмотрите результат:
```javascript
console.log ( new Blob ( [ 
    '01101000110000100000011101011010010001000100011101011' 
] ) )
console.log ( new Blob ( [ 
    '01101000110000100000011101011010010001000100011101011', 
    '01101000110000100000011101011010010001000100011101011' 
] ) )
```
:coffee: :two: Закиньте в консоль следующий код:
```javascript
fetch ( 'https://avatars2.githubusercontent.com/u/46?v=4' )
   .then ( response => {
      response.arrayBuffer()
         .then ( response => {
            console.log ( new Blob ( [ response ] ) )
         })
   })
```
:coffee: :three: Закиньте в консоль следующий код:
```javascript
var picture = document.createElement ( 'img' )
document.body.appendChild ( picture )

fetch ( 'https://avatars2.githubusercontent.com/u/46?v=4' )
   .then ( response => {
      response.arrayBuffer()
         .then ( response => {
            var pixels = new Uint8Array( response )
    	    urlObject = URL.createObjectURL( new Blob ( [ response ] ))
    	    picture.src = urlObject
      })
   })
```

| Свойства | объекта Response |
|-|-|
| **`type`** | `строка, содержащая тип данных ( "basic" — все ОК )` |
| **`url`** | `URL адрес ответа сервера` |
| **`status`** | `код статуса ответа сервера` |
| **`statusText`** | `текст статуса ответа сервера` |
| **`ok`** | `логическое выражение; принимает значение true, если получение данных произошло без ошибок ( status от 200 до 299 )` |
| **`bodyUsed`** | `логическое выражение; принимает значение true, если body загружено` |

:coffee: :four:

```javascript
fetch ( 'https://httpbin.org/get' )
    .then ( response => response.json()
        .then ( 
            response => 
                console.log ( response.headers )
        )
    )
```
```console
▼ {Accept: "*/*", Accept-Encoding: "gzip, deflate, br", Accept-Language: "en-US,en;q=0.9,ru;q=0.8", Connection: "close", Host: "httpbin.org", …}
   Accept: "*/*"
   Accept-Encoding: "gzip, deflate, br"
   Accept-Language: "en-US,en;q=0.9,ru;q=0.8"
   Connection: "close"
   Host: "httpbin.org"
   Origin: "null"
   Save-Data: "on"
   User-Agent: "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36"
 ► __proto__: Object
```

:coffee: :five:
Сделаем кросс-доменный запрос:
```javascript
var request = new Request ( 
    'https://httpbin.org/post',
    {
        method: 'POST', 
        mode: 'cors', 
        redirect: 'follow',
        headers: new Headers({
            'Content-Type': 'text/plain'
        }),
        body: "Hello, students!"
    }
)

fetch( request )
    .then ( response => {
        console.log ( response )
        response.json()
            .then ( x => console.log ( x ) )
    })
```
Ответ сервера:

###### Объект Response
```console
▼ Response {type: "cors", url: "https://httpbin.org/post", redirected: false, status: 200, ok: true, …}
    body: (...)
    bodyUsed: true
  ► headers: Headers {}
    ok: true
    redirected: false
    status: 200
    statusText: "OK"
    type: "cors"
    url: "https://httpbin.org/post"
  ► __proto__: Response
```
###### распарсенный как json:
```console
▼ {args: {…}, data: "Hello, students!", files: {…}, form: {…}, headers: {…}, …}
  ► args: {}
    data: "Hello, students!"
  ► files: {}
  ► form: {}
  ► headers: {Accept: "*/*", Accept-Encoding: "gzip, deflate, br", Accept-Language: "en-US,en;q=0.9,ru;q=0.8", Connection: "close", Content-Length: "16", …}
    json: null
    origin: "185.38.217.69"
    url: "https://httpbin.org/post"
  ► __proto__: Object
```

### [:briefcase: Упражнения](https://docs.google.com/forms/d/e/1FAIpQLSf3Qcz6-DrAlgTLqpy-tZGiARxm80cdnQmvga-Oj6xGvONXTA/viewform)