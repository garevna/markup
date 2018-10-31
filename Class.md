# :mortar_board: Классы
###### ES6 ( ECMAScript 2015 )
Синтаксический сахар на поверхности прототипной модели наследования

:warning: Код внутри тела класса всегда выполняется в **`strict mode`**<br/>
`( даже если вы не использовали директиву **_'use strict'_** )`

:warning: "Тело" класса всегда заключено в фигурные скобки `{` `}`

Внутри фигурных скобок объявляются конструктор ( **_constructor_** ) и методы класса

Метод **_constructor_** создает и инициализирует экземпляра класса

:warning: Все собственные свойства экземпляра должны быть объявлены в конструкторе  **_constructor()_**

⚠️ В классах можно объявить только публичные свойства <br/>
`( приватных нет )`
***
### :mortar_board: class declaration
###### :no_entry_sign: hoisting
`объявление класса дожно быть раньше первого обращения к нему`

Классы - это специальные функции-"обертки", в которые "заворачивают" конструктор
###### :coffee: :one:
```javascript
class Picture {
    constructor ( url, width ) {
        this.elem = document.createElement ( 'img' )
        this.elem.src = url
        this.width = width
    }
}

typeof Picture  // "function"
```
> :warning: объявленный класс невозможно удалить динамически, без перезагрузки страницы<br/>
> В примере :one: идентификатор  **_Picture_**  уже занят, и никакие магические заклинания не помогут переопределить его  содержание

> :warning: если обычный конструктор JS можно вызвать и как функцию, и как конструктор ( с ключевым словом `new` ), 
то конструктор класса вызвать без ключевого слова `new`  нельзя - будет сгенерировано исключение **_TypeError_**
```javascript
let x = new Picture ( "http://www.radioactiva.cl/wp-content/uploads/2018/05/pikachu.jpg", 200 )
document.body.appendChild ( x.elem )
```
***
### :mortar_board: class expression
###### еще один способ определить класс
###### class expression может быть именованным или аниномным

#### Примеры именованных классов
###### :coffee: :two:
```javascript
let Picture = class {
    constructor () {
        this.canvas = document.createElement ( 'canvas' )
        document.body.appendChild ( this.canvas )
        this.area = this.canvas.getContext ( "2d" )
    }
}

Picture.name   // "Picture"
```
###### :coffee: :three:
```javascript
let Picture = class Canvas {
    constructor () {
        this.canvas = document.createElement ( 'canvas' )
        document.body.appendChild ( this.canvas )
        this.area = this.canvas.getContext ( "2d" )
    }
}

Picture.name   // "Canvas"
```
* Имя _class expression_ является локальным для тела класса
* Оно доступно как свойство  **_name_**  класса
* Из экземпляра  picture  класса можно получить имя класса так:
```javascript
picture.__proto__.constructor.name   // "Canvas"
```
#### Пример анонимного класса
###### :coffee: :four:
```javascript
let pict = new class {
    constructor () {
        this.canvas = document.createElement ( 'canvas' )
        document.body.appendChild ( this.canvas )
        this.area = this.canvas.getContext ( "2d" )
    }
} ()
```
здесь мы создаем экземпляр  **_pict_**  анонимного класса
```javascript
pict.__proto__.constructor.name  // ""
```
###### :coffee: :five:
```javascript
const Sample = class Canvas {
    constructor () {
        this.canvas = document.createElement ( 'canvas' )
        document.body.appendChild ( this.canvas )
        this.resizeCanvas()
        this.canvas.style.border = "1px solid #000000"
        this.area = this.canvas.getContext ( "2d" )
    }
    resizeCanvas ( event ) {
        this.canvas.width = window.innerWidth - 30
        this.canvas.height = window.innerHeight - 20
    }
    drawLine ( points ) {
        this.area.moveTo( points[0].x, points[0].y )
        this.area.lineTo( points[1].x, points[1].y )
        this.area.stroke()
    }
}

let pict = new Sample ()
window.onresize = pict.resizeCanvas.bind ( pict )
pict.drawLine ( [ { x: 50, y: 50 }, { x: 250, y: 250 } ] )
pict.drawLine (  [ { x: 250, y: 250 }, { x: 100, y: 250 } ] )
```
:pushpin: Чтобы получить имя класса, нужно использовать его свойство  **name**:
```javascript
console.log ( Sample.name ) // "Canvas"
```
***
### :mortar_board: Потеря контекста
###### :pushpin: В строгом режиме не происходит неявной передачи контекста вызова 

:warning: Потеря контекста происходит всегда, если ссылка на метод передается в новую переменную:
```javascript
     let drawLine = pict.drawLine
     drawLine ( [ { x: 50, y: 50 }, { x: 250, y: 250 } ] )
```
будет сгенерировано исключение:
```console
⛔️ Uncaught TypeError: Cannot read property 'area' of undefined
```
Передачу контекста вызова нужно сделать явным образом:
```javascript
let drawLine = pict.drawLine.bind ( pict )
```
> :pushpin: Потеря контекста ( undefined ) происходит вследствие того, что весь код внутри тела класса выполняется в  strict mode, хотя явного указания  'use strict'  в коде класса нет

> При отсутствии явного указания на объект, вызывающий метод, <br/>
> в строгом режиме `this` не будет ссылкой на глобальный объект  `window`<br/>
> В строгом режиме `this` будет  `undefined`
***
## :mortar_board: static

Статические методы класса объявляются с помощью ключевого слова **static**

Эти методы могут быть вызваны только как методы класса

:warning: Внутри статического метода `this` указывает на конструктор класса, а не на экземпляр

###### [:coffee: :six:](Class-sample-6) 
###### [:coffee: :seven:](Class-sample-7) 