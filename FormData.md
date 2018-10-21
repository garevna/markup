# :mortar_board: FormData

###### конструктор FormData() создает объект класса **FormData**

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

* Объекты класса **FormData** предоставляют интефейс для манипулирования данными
* Объекты класса **FormData** могут быть отправлены на сервер с помощью `XMLHttpRequest` или `Fetch API`

## Методы

| append | delete | get | set |
|-|-|-|-|

### append()

Принимает два аргумента - имя ключа и его значение

добавляет пару ключ/значение в форму

```javascript
var formData = new FormData()
formData.append ( "username", "garevna" )
formData.append ( "token", "HgTY78-jdfhj91*/jskdfj" )
```
### get()
```javascript
formData.get ( "username" )  // "garevna"
formData.get ( "token" )     // "HgTY78-jdfhj91*/jskdfj"
```
### has()
```javascript
formData.has ( "token" )     // true
```
### set()
```javascript
formData.set ( "token", "gF&op*i91/54gkjHU" )
formData.get ( "token" )  // "gF&op*i91/54gkjHU"
```
### delete()
```javascript
formData.delete ( "token" )
formData.get ("token")    // null
```
## fetch data

:coffee: :one:

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
:coffee: :two:

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
:coffee: :three:

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
