### :briefcase: Упражнение 2

Создадим новый файл :pencil: _promise.js_  в папке :open_file_folder: src

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
<img src="https://github.com/garevna/js-course/blob/master/images/git-bush-ico.png?raw=true" width="22"/> в Git Bush запустим команду `webpack`

![](https://lh5.googleusercontent.com/zhM1TwRySgAAGrg8ts-n8mvlACifQXHzQudaUs37ce45AtHM9VjMa8CswyohFhG0y9p9sV15jw_rqV8hyOMGX62y5o829hATXLXNLPEN8h779mjS2yC140CdCuwFMvqYGhcu-b9lD1lvquQ)

Теперь откройте файл **_index.html_** в окне браузера