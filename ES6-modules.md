# :mortar_board: ES6 модули

[:small_orange_diamond: **export**](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Statements/export)<br/>
[:small_orange_diamond: **import**](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Statements/import)
***
Модули - "строительные блоки" приложения

Создаются JS-модули путем экспорта содержимого JS-файла ( :small_orange_diamond: **`export`** )

Директива :small_orange_diamond: **`import`**  позволяет вставить модуль, созданный с помощью `export`, в другой JS-файл

`( при использовании  webpack  для сборки приложения поддержка браузерами ES6 модулей не имеет значения - вебпак сделает все правильно 😉 )`

## :mortar_board: export

#### :radio_button: Именованный экспорт 
###### ( несколько экспортов из одного файла )
###### :pencil: файл lib.js:
```javascript
export const sqrt = Math.sqrt

export function buildElement ( tagName ) {
    return document.body.appendChild (
        document.createElement ( tagName )
    ) 
}

export function elemExist ( elemSelector ) {
    return !!document.querySelector ( elemSelector )
}
```
#### :radio_button: Дефолтный экспорт 
###### Экспорт по умолчанию - это экспорт единственного объекта
###### ( один "главный" объект в модуле )
###### :pencil: файл Sample.js:
```javascript
const Sample = function ( tagName ) {
    this.elem = document.body.appendChild (
        document.createElement ( tagName )
    ) 
}
Sample.prototype.getAttrs = function () {
    return Object.getOwnPropertyNames ( this.elem )
}
Sample.prototype.setAttr = function ( attr, val ) {
    this.elem [ attr ] = val
}
Sample.prototype.setStyle = function ( css_attr, val ) {
    this.elem.style [ css_attr ] = val
}

export default Sample
```

## :mortar_board: import

При импорте из **_js_**-файлов расширение файла указывать не обязательно

### :coffee:  Импорт именованного экспорта
 
Предположим, нам нужно использовать функции  **_buildElement_**  и  **_elemExist_**  из файла  **lib.js**  ( см. выше )
в файл **main.js**

###### :pencil: main.js:
```javascript
import { buildElement, elemExist } from 'lib'
```
:ballot_box_with_check: Можно импортировать все содержимое файла lib.js:
```javascript
import * as lib from 'lib'
```
✍ Теперь можно использовать функции **_buildElement_**  и  **_elemExist_**:
```javascript
var picture = buildElement ( 'img' )
picture.src = 'http://cs5-2.4pda.to/8853638.gif'

console.log ( elemExist ( picture.tagName ) )
```
### :coffee: Импорт дефолтного экспорта

Теперь импортируем из файла  **sample.js**  ( см. выше ) в файл  **main.js**:
```javascript
import Sample from 'Sample';
let sample = new Sample ()
```