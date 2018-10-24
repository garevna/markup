| [:rewind:](FormData) |
|-|

:coffee:

Создадим форму с атрибутом **name**, имеющим значение **_upload_file_**, 

и элемент **img**, значение атрибута **name** которого будет **_picture_**
```html
<form enctype="multipart/form-data" 
      method="post" 
      name="upload_file"
>
    <input type="email" 
           autocomplete="on" 
           name="user_email" 
           placeholder="email" 
    >
    <br>
    <input type="file" name="file">

    <input type="submit" value="Upload">
</form>

<img name = "picture"/>
```

Получим данные формы после заполнения и отправим на сервер

```javascript
var form = document.forms.namedItem ( "upload_file" )
form.addEventListener( 'submit', function ( event ) {

    event.preventDefault()
    var data = new FormData(form)
    data.append ( "comment", "Hello everybody!" )

    var request = new XMLHttpRequest()
    request.open ( "POST", "https://httpbin.org/post" )
    request.onload = function( event ) {
       console.log ( 
          JSON.parse ( this.responseText ).files.file
       )
       document.images.namedItem ( "img" ) .src = 
          JSON.parse ( this.responseText ).files.file
    }

    request.send( data )

}, false )
```
###### Посмотрим результат в панели Network браузера
![](https://github.com/garevna/js-course/blob/master/images/lessons/b0d4d73f21508dd67e0c57a590f582f0%5B1%5D.png?raw=true)

###### Заглянем во вкладку _Response_ вкладки _Network_
```
{
  "args": {}, 
  "data": "", 
  "files": {
    "file": "data:image/png;base64,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"
  }, 
  "form": {
    "comment": "Hello everybody!", 
    "user_email": "garevna@gmail.com"
  }, 
  "headers": {
    "Accept": "*/*", 
    "Accept-Encoding": "gzip, deflate, br", 
    "Accept-Language": "en-US,en;q=0.9,ru;q=0.8", 
    "Connection": "close", 
    "Content-Length": "2343", 
    "Content-Type": "multipart/form-data; boundary=----WebKitFormBoundaryunBnviC7lbTvk5ku", 
    "Host": "httpbin.org", 
    "Origin": "https://replbox.repl.it", 
    "Referer": "https://replbox.repl.it/data/web_hosting_1/garevna/FormData/", 
    "Save-Data": "on", 
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36"
  }, 
  "json": null, 
  "origin": "185.38.217.69", 
  "url": "https://httpbin.org/post"
}
```

| [:rewind:](FormData) |
|-|