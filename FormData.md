# :mortar_board: FormData

## :mortar_board: FormData()
Конструктор FormData() создает объект класса **_FormData_**

```console
▼ FormData {}
  ▼ __proto__: FormData
      ► append: ƒ append()
      ► delete: ƒ delete()
      ► entries: ƒ entries()
      ► forEach: ƒ forEach()
      ► get: ƒ ()
      ► getAll: ƒ getAll()
      ► has: ƒ has()
      ► keys: ƒ keys()
      ► set: ƒ ()
      ► values: ƒ values()
      ► constructor: ƒ FormData()
      ► Symbol(Symbol.iterator): ƒ entries()
        Symbol(Symbol.toStringTag): "FormData"
      ► __proto__: Object
```

```javascript
var formData = new FormData()
formData instanceof FormData   // true
```

:clipboard: Объекты класса **FormData** предоставляют интефейс для манипулирования данными форм и могут быть отправлены на сервер с помощью `XMLHttpRequest` или `Fetch API`

## Методы

| append | delete | get | set |
|-|-|-|-|

### append()

Принимает два аргумента - имя ключа и его значение

Если такого ключа еще нет, добавляет пару ключ/значение

Если такой ключ уже существует, добавляет ему новое значение

```javascript
var formData = new FormData()
formData.append ( "username", "garevna" )
formData.append ( "token", "HgTY78-jdfhj91*/jskdfj" )
```
### has()
```javascript
formData.has ( "token" )     // true
```
### get()
```javascript
formData.get ( "username" )  // "garevna"
formData.get ( "token" )     // "HgTY78-jdfhj91*/jskdfj"
```
### getAll()
Возвращает массив всех значений, связанных с указанным в аргументе ключом
```javascript
formData.append ( "pictures", "http://icecream.me/uploads/b0d4d73f21508dd67e0c57a590f582f0.png" )
formData.getAll ( "pictures" )
formData.append ( "pictures", "https://github.com/garevna/js-course/raw/master/images/js_cup-ico.png" )
formData.getAll ( "pictures" )
```
### set()
Аргументы: ключ, значение

Если указанный аргументом ключ уже существует, устанавливает ему новое значение, в противном случае добавляет новый ключ и значение 
```javascript
formData.set ( "token", "gF&op*i91/54gkjHU" )
formData.get ( "token" )  // "gF&op*i91/54gkjHU"
```
### delete()
```javascript
formData.delete ( "token" )
formData.get ("token")    // null
```
### keys()

Возвращает объект-итератор ( будем изучать позже )

### entries()

Возвращает объект-итератор ( будем изучать позже )

:coffee: :one:
```javascript
var iterator = formData.keys()
iterator.next()
iterator.next()
...
```
:coffee: :two:
```javascript
var iterator = formData.keys()
iterator.next()
iterator.next()
...
```
***
## fetch data

:coffee: :three:

```javascript
var fileSelector = document.body.appendChild (
   document.createElement ( 'input' )
)
fileSelector.type = "file"

let formData = new FormData()

fileSelector.onchange = function ( event ) {
    formData.append ( "avatar", this.files[0] )
    console.log ( formData.get ( "avatar" ) )
}
```
:coffee: :four:

```javascript
var fileSelector = document.body.appendChild (
   document.createElement ( 'input' )
)
fileSelector.type = "file"

fileSelector.onchange = function ( event ) {
    let file = this.files[0]
    if ( file.type.indexOf ( 'image/' ) >= 0 ) {
        var reader = new FileReader ()
        reader.readAsArrayBuffer ( file )
        reader.onload = function ( event ) {
            fetch ( 'https://httpbin.org/post', {
                method: 'POST',
                headers: {
                    'Content-Type': file.type
                },
                body: new Blob ( [ this.result ], { type: file.type } )
            })
            .then ( response => console.log ( response ) )
        }
    }
}
```
:coffee: :five:

:warning: Для выполнения упражнения перейдем на страницу http://ptsv2.com

###### Загрузим изображение с клиента: 
```javascript
var fileSelector = document.body.appendChild (
   document.createElement ( 'input' )
)
fileSelector.type = "file"

fileSelector.onchange = function ( event ) {
    let file = this.files[0]
    if ( file.type.indexOf ( 'image/' ) >= 0 ) {
        var reader = new FileReader ()
        reader.readAsArrayBuffer ( file )
        reader.onload = function ( event ) {
            fetch ( 'http://ptsv2.com/t/garevna/post', {
                method: 'POST',
                headers: {
                    'Content-Type': file.type
                },
                body: new Blob ( [ this.result ], { type: file.type } )
            })
            .then ( response => response.json()
               .then ( response => console.log ( response ) )
            )
        }
    }
}
```
###### прочитаем записанное:
```javascript
fetch ( 'http://ptsv2.com/t/garevna/d/890001/json')
   .then ( response => {
      let reader = response.body.getReader()
      reader.read( response.body )
         .then ( result => console.log ( result ) )
   })
