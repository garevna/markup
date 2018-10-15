## :briefcase: Упражнения
Далее мы будем использовать фейковые серверы для апробирования методов  **`XMLHttpRequest()`**

* https://httpbin.org
* http://ptsv2.com

Эти ресурсы не требуют аутентификации, они предназначены исключительно для целей тестирования

:coffee: :one:

###### POST ( _`application/x-www-form-urlencoded`_ )

```javascript
var request = new XMLHttpRequest()
request.open (
    "POST",
    'https://httpbin.org/post',
    true 
)

request.setRequestHeader (
    "Content-Type",
    "application/x-www-form-urlencoded"
)

request.onreadystatechange = function() {
   if (
      this.readyState === 4
      && this.status === 200 
   ) {
        console.log ( 'success' )
        console.log ( this.responseText )
   }
}
request.send ( "name=garevna&speciality=frontEnd" )
```
Результат в консоли:
```console
success
{
  "args": {}, 
  "data": "", 
  "files": {}, 
  "form": {
    "name": "garevna", 
    "speciality": "frontEnd"
  }, 
  "headers": {
    "Accept": "*/*", 
    "Accept-Encoding": "gzip, deflate, br", 
    "Accept-Language": "en-US,en;q=0.9,ru;q=0.8", 
    "Connection": "close", 
    "Content-Length": "32", 
    "Content-Type": "application/x-www-form-urlencoded", 
    "Host": "httpbin.org", 
    "Origin": "null", 
    "Save-Data": "on", 
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36"
  }, 
  "json": null, 
  "origin": "185.38.217.69", 
  "url": "https://httpbin.org/post"
}
```
***
<table>
    <tr>
        <td rowspan="4">
            <img src="https://orig00.deviantart.net/bf33/f/2014/354/6/0/free_toilet_pose_for_chatlands_by_warriorcatsbluepelt-d8ajdq4.png">
        </td>
    </tr>
    <tr>
        <td><code>
            ⚠️ Прежде, чем приступить к выполнению следующих упражнений, 
            создайте свой <a href="http://ptsv2.com">Toilet</a></code>
        </td>
    </tr>
    <tr>
        <td><code>
            ⚠️ Вместо <em>garevna</em> в своих запросах вставляйте название своего <b>Toilet</b></code>
        </td>
    </tr>
    <tr>
        <td><code>
            ⚠️ Дальнейший код  нужно выполнять в консоли того же окна, 
            где будет открыт <a href="http://ptsv2.com"><b>ресурс</b></a></code>
        </td>
    </tr>
<table>

***

⚠️ При несоответствии протокола  ваш запрос будет отклонен:
```console
⛔️ Mixed Content: 
The page at ... was loaded over HTTPS, 
but requested an insecure XMLHttpRequest endpoint 
'http://ptsv2.com/t/.../post'
This request has been blocked; 
the content must be served over HTTPS
```
⚠️ Запрос из консоли любого другого ресурса с протоколом http будет кросс-доменным, поэтому тоже будет заблокирован браузером ( политика безопасности )
```console
⛔️ Failed to load http://ptsv2.com/t/.../post: 
No 'Access-Control-Allow-Origin' header 
is present on the requested resource
Origin ... is therefore not allowed access
```
***
:coffee: :two:

###### POST ( _`application/x-www-form-urlencoded`_ )

```javascript
var transport = new XMLHttpRequest()
transport.open (
    "POST",
    'http://ptsv2.com/t/garevna/post',
    true
)

transport.setRequestHeader (
    "Content-Type",
    "application/x-www-form-urlencoded" 
)

transport.onreadystatechange = function() {
   if( this.readyState === XMLHttpRequest.DONE &&
       this.status === 200 ) {
        console.log ( 'success' )
        console.log ( this.responseText )
   }
}
transport.send ( "name=garevna&speciality=frontEnd" )
```
***
:coffee: :three:

###### POST ( _`application/json`_ )

```javascript
var transport = new XMLHttpRequest()
transport.open (
    "POST",
    'http://ptsv2.com/t/garevna/post',
    true
)

transport.setRequestHeader (
    "Content-Type",
    "application/json" 
)

transport.onreadystatechange = function() {
    if( this.readyState === XMLHttpRequest.DONE && 
        this.status === 200 ) {
        console.log ( 'success' )
    }
}
transport.send (
    JSON.stringify (
        {
            title: "Show",
            text: 'must go on'
        }
    )
)
```
:coffee: :four:

###### POST ( _`text/plain`_ )

```javascript
var transport = new XMLHttpRequest()
transport.open (
    "POST",
    'http://ptsv2.com/t/garevna/post',
    true
)

transport.setRequestHeader (
    "Content-Type",
    "text/plain" 
)

transport.onreadystatechange = function() {
    if( this.readyState === XMLHttpRequest.DONE && 
        this.status === 200 ) {
        console.log ( 'success' )
    }
}
transport.send( "Show must go on" )
```