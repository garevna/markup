### :briefcase: Упражнение 2

###### Создадим новый файл :pencil: _promise.js_  в папке :open_file_folder: src

###### :pencil: promise.js
```javascript
var promise = new Promise ( function ( resolve, reject ) {
    document.write ( 'Wait, pease...<br>' )
    setTimeout ( () => resolve ( "OK, you are here ?" ), 2000 )
})

export default promise
```
###### :pencil: index.js
```javascript
import promise from './promise.js'

promise.then ( response =>
    document.querySelector ( '.sampleClass' )
        .innerText += response )
```
###### <img src="https://gitforwindows.org/img/gwindows_logo.png" width="22"/> в Git Bush запустим команду webpack
###### Теперь откройте файл index.html в окне браузера