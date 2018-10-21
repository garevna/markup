#### CSRF

**Сross Site Request Forgery** ( межсайтовая подделка запроса )

Когда юзер заходит на сайт, созданный злоумышленником, от его лица может быть отправлен запрос на другой сервер, на котором юзер аутентифицирован

CSRF-атака возможна только в том случае, если сервер не требует обязательного включения в запрос подтверждения  со стороны юзера, которое не может подделано атакующим скриптом

Для защиты от CSRF-атак можно использовать заголовок **X-CSRF-TOKEN**

* Токен должен быть предоставлен сервером
* Его можно записать в куки на клиенте
* При отправке запроса можно добавить заголовок **X-CSRF-TOKEN** со значением токена, предоставленным сервером

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