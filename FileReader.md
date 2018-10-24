## :mortar_board: FileReader

###### Конструктор

Создает экземпляр объекта, который позволяет веб-приложению асинхронно читать содержимое файлов ( объекты класса **_File_** ) на компьютере пользователя или объекты класса **_Blob_**

:warning: Не может читать объекты класса **_ReadableStream_**

```javascript
var reader = new FileReader ()
```
###### Методы
```javascript
ƒ readAsArrayBuffer()
ƒ readAsBinaryString()
ƒ readAsDataURL()
ƒ readAsText()
```
###### Свойства

✅ error 
```
объект DOMError со свойствами name и message
```
✅ readyState
```
✋ EMPTY   : 0 ( данные еще не загружены )
✋ LOADING : 1 ( данные загружаются )
✋ DONE    : 2 ( операция чтения завершена )
```
✅ result
```
данные
✋ значение свойства result определено только после завершения операции чтения
✋ формат данных зависит от способа, с помощью которого процесс был вызван
```
⏰ `Обработка событий`
```javascript
✅ onabort
✅ onerror
✅ onload
✅ onloadend
✅ onloadstart
✅ onprogress
```

:coffee: :one:

✍ Разберите работу кода в Chrome DevTools:
```javascript
var selector = document.body.appendChild ( document.createElement ( 'input' ) )
selector.type = 'file'

selector.onchange = function handleFiles( event ) {
        fileReader.readAsDataURL ( event.target.files [0] )
        fileReader.onload = function ( event ) {
                picture.src = event.target.result
        }
}

var picture = document.body.appendChild ( document.createElement ( 'img' ) )

var fileReader = new FileReader ()
```
Сравните с уже знакомым методом  URL.createObjectURL:
```javascript
picture.src = URL.createObjectURL( selected )
```
:coffee: :two:

✍ Разберите работу кода в Chrome DevTools:
```javascript
var selector = document.body.appendChild (
    document.createElement ( 'input' )
)
selector.type = 'file'

selector.onchange = function handleFiles( event ) {
    var selected = event.target.files [0]
    header.innerText =  selected.type
    switch ( selected.type.split('/')[0] ) {
        case 'image':
            fileReader.readAsDataURL ( selected )
            fileReader.onload = function ( event ) {
                picture.src = event.target.result
            }
            break
        case 'text' :
            fileReader.readAsText ( selected )
            fileReader.onload = function ( event ) {
                demo.innerText = event.target.result
            }
            break
        case 'application':
            fileReader.readAsText ( selected )
            fileReader.onload = function ( event ) {
                demo.innerText = event.target.result
            }
            break
        default: 
            fileReader.readAsArrayBuffer ( selected )
            fileReader.onload = function ( event ) {
                console.log ( event.target.result )
            }
            break
    }
}

var picture = document.body.appendChild (
    document.createElement ( 'img' )
)
var header = document.body.appendChild (
    document.createElement ( 'h3' )
)
var demo = document.body.appendChild (
    document.createElement ( 'pre' )
)
var fileReader = new FileReader ()
```
:coffee: :three:

✍ Разберите работу кода в Chrome DevTools:
```javascript
var selector = document.body.appendChild ( document.createElement ( 'input' ) )
selector.type = 'file'
selector.multiple = true
selector.id = 'selectImages'
selector.style.display = 'none'

var label = document.body.appendChild ( document.createElement ( 'label' ) )
label.htmlFor = 'selectImages'
label.innerText = 'Select images'

selector.onchange = function ( event ) {
    for ( var file of event.target.files ) {
        if ( file.type.split('/')[0] !== 'image' ) return
        var picture = document.createElement ( "img" )
        picture.file = file
        document.body.appendChild( picture )
        var fileReader = new FileReader ()
        fileReader.onload = ( 
            image => function ( e ) {
                image.src = e.target.result
            } 
        )( picture )
        fileReader.readAsDataURL ( file )
    }
}
```