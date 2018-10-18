# :mortar_board: Fetch API

Интерфейс Fetch API 

| | |
|-|-|
| [:arrow_right_hook: Request](#mortar_board-request) | |
| [:arrow_right_hook: Response](#mortar_board-response) | ✅ json () |
|             | ✅ text () |
|             | ✅ blob () |
|             | ✅ arrayBuffer() |
| ✅ URL.createObjectURL() | |


Метод **`fetch`** объекта `window` реализует AJAX-запросы на основе промисов, что является его главным отличием от **`XMLHttpRequest`**

Кроме того, в отличие от **`XMLHttpRequest`**, метод **`fetch`** осуществляет только асинхронные запросы

Метод **`fetch`** возвращает **_промис_**

Обязательный первый аргумент метода **`fetch`** - это url ресурса
```javascript
fetch ( "message.txt" )
    .then ( response => {
        ...
    })
```
Когда промис завершится, он вернет объект **`Response`**

## :mortar_board: Request

Выведите в консоль объект Request
```javascript
console.dir ( Request )
```

Объект запроса

| Свойства | Значения | |
|-|-|-|
| **`method`** | `✅ GET` | |
| | `✅ POST` | |
| | `✅ PUT` | |
| | `✅ DELETE` | |
| | `✅ HEAD` | |
| **`url`** | | `url  запрошенного ресурса` |
| **`headers`** | | `заголовки запроса` |
| **`referrer`** | | `источник запроса` |
| **`mode`** | `✅ cors` | |
| | `✅ no-cors` | |
| | `✅ same-origin` | |
| **`credentials`** | `✅ omit` | `должны ли файлы cookie отправляться с запросом` |
| | `✅ same-origin` | |
| **`redirect`** | | `✅ follow` |
| | `✅ error` | |
| | `✅ manual` | |
| **`integrity`** | | `дайджест ресурса` |
| **`cache`** | `режим кэширования` | `✅ default` |
| | `✅ reload` | |
| | `✅ no-cache` | |

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

| Методы | возвращают промис, результатом которого будет |
|-|-|
| **`arrayBuffer()`** | `ArrayBuffer ( строка из нулей и единиц )`
| **`blob()`** | `объект Blob ( данные в двоичном формате )` |
| **`clone()`** | `копию объекта Response` |
| **`formData()`** | `данные FormData` |
| **`json()`** | `данные в JSON-формате` |
| **`text()`** | `данные в текстовом формате` |

 объекта Response:

| Свойства |  |
|-|-|
| **`type`** | `строка, содержащая тип данных ( "basic" — все ОК )` |
| **`url`** | `URL адрес ответа сервера` |
| **`status`** | `код статуса ответа сервера` |
| **`statusText`** | `текст статуса ответа сервера` |
| **`ok`** | `логическое выражение; принимает значение true, если получение данных произошло без ошибок ( status от 200 до 299 )` |
| **`bodyUsed`** | логическое выражение; принимает значение true, если body загружено |

:coffee: :two:
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

## :mortar_board: Origin

В заголовках ответа сервера ( объект **`headers`** ) есть свойство **`Host`** ( *куда был направлен запрос* ) и свойство **`Origin`** ( указывает на домен, *с которого пришел запрос* )

Свойство **`Referer`** указывает *полный адрес* ресурса, с которого пришел запрос

Если сделать запрос с пустой страницы ( не имеющей адреса в сети ), то в заголовках ответа сервера свойство **`Origin`** будет иметь значение `null`, а свойство **`Referer`**  будет отсутствовать
