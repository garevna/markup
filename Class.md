# :mortar_board: Классы
###### ES6 ( ECMAScript 2015 )
Синтаксический сахар на поверхности прототипной модели наследования

| [class declaration](#mortar_board-class-declaration) | [class expression](#mortar_board-class-expression) |
|-|-|
| [**`Потеря контекста`**](#context) | [**static**](Class-static) | 
| [ **get & set** ](Class-get-set) | [**extends**](Class-extends) |
| [**super**](Class-super) | [:coffee: **`Пример`**](Class-sample) |

:warning: Код внутри тела класса всегда выполняется в **`strict mode`**<br/>
`( даже если вы не использовали директиву **_'use strict'_** )`

:warning: "Тело" класса всегда заключено в фигурные скобки `{` `}`

Внутри фигурных скобок объявляются конструктор ( **_constructor_** ) и методы класса

Метод **_constructor_** создает и инициализирует экземпляра класса

:warning: Все собственные свойства экземпляра должны быть объявлены в конструкторе  **_constructor()_**

"Под капотом" работает все та же прототипная модель наследования JS

Создаваемые в конструкторе класса свойства и методы могут быть приватными и публичными<br/>
( как и в обычном конструкторе )

В обычном конструкторе контекстом вызова приватных методов будет глобальный объект `window`

В конструкторе класса приватные методы теряют контекст ( `undefined` )

```javascript
class User {
    constructor ( name ) {
        var privateVar = prompt ( "Set privateVar value: " )
        function showPrivate () {
            console.log ( `Ай-яй-яй, у меня контекст вызова ${this}` )
            console.log ( `Зато я вижу приватную переменную: ${privateVar}` )
        }
        this.name = name || "Бегемот"
        this.show = function () {
            showPrivate ()
        }
    }
}

var user = new User ( "Крокодил" )
user.show()
```
###### Result
```console
Ай-яй-яй, у меня контекст вызова undefined
Зато я вижу приватную переменную: 789
```
Для того, чтобы избавиться от иллюзий по поводу "классов" в JS,<br/>
создадим аналогичный экземпляр с помощью обычного конструктора
```javascript
function User ( name ) {
    var privateVar = prompt ( "Set privateVar value: " )
    function showPrivate () {
        console.log ( `Ай-яй-яй, у меня контекст вызова ${this}` )
        console.log ( `Зато я вижу приватную переменную: ${privateVar}` )
    }
    this.name = name || "Бегемот"
    this.show = function () {
        showPrivate ()
    }
}

var user = new User ( "Крокодил" )
user.show()
```
###### Result
```console
Ай-яй-яй, у меня контекст вызова [object Window]
Зато я вижу приватную переменную: 789
```
Выведем в консоль оба варианта **user** и найдем те косметические отличия, которые там должны быть :wink:

* `constructor: class User`    /    `constructor: ƒ User( name )`
***
### :mortar_board: class declaration

| [:arrow_double_up:](#es6--ecmascript-2015-) |
|-|

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

| [:arrow_double_up:](#es6--ecmascript-2015-) |
|-|

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
<a name="context"></a>
### :mortar_board: Потеря контекста

| [:arrow_double_up:](#es6--ecmascript-2015-) |
|-|

###### :pushpin: В строгом режиме не происходит неявной передачи контекста вызова 

:warning: Потеря контекста происходит всегда, если ссылка на метод передается в новую переменную:

###### :coffee: :six:
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

:coffee: :seven:

В этом примере контекст теряется в функции **_getProp()_**,<br/>
объявленной внутри метода **_addSomeInfo_**<br/>
( внутренняя функция не наследует контекст вызова родительской )<br/>
```javascript
class User {
    constructor ( name ) {
        this.name = name || 'unknown'
    }
    addSomeInfo ( props ) {
        if ( !Array.isArray ( props ) ) return
        function getProp ( prop ) {
            this [ prop.name ] = prop.value
        }
        for ( var prop of props ) {
            getProp ( prop )
        }
    }
}
```
Создадим экземпляр **user** класса **User**<br/>
и вызовем метод **_addSomeInfo_**<br/>
в контексте объекта **user**
```javascript
var user = new User ( "Grig" )
user.addSomeInfo ([
    { name: "age", value: 25 },
    { name: "hobby", value: [ "football", "fishing" ] }
])
```
###### :scream_cat: Результат
```console
⛔️ Uncaught TypeError: Cannot set property 'age' of undefined
```
:heavy_exclamation_mark: Внутри функции **_getProp_** контекст вызова ( **`this`** ) оказался `undefined`

Теперь используем стрелочную функцию **_getProp_**, которая не теряет контекст :wink:
```javascript
class User {
    constructor ( name ) {
        this.name = name || 'unknown'
    }
    addSomeInfo ( props ) {
        if ( !Array.isArray ( props ) ) return
        var getProp = prop => this [ prop.name ] = prop.value
        for ( var prop of props ) {
            getProp ( prop )
        }
    }
}
```
Создадим экземпляр **user** и вызовем метод **_addSomeInfo_**<br/>
```javascript
var user = new User ( "Grig" )
user.addSomeInfo ([
    { name: "age", value: 25 },
    { name: "hobby", value: [ "football", "fishing" ] }
])
console.log ( user )
```
###### :scream_cat: Результат
```console
▼ User {name: "Grig", age: 25, hobby: Array(2)}
    age: 25
  ► hobby: (2) ["football", "fishing"]
    name: "Grig"
  ▼ __proto__:
      ► addSomeInfo: addSomeInfo ( props ) { if ( !Array.isArray ( props ) ) return var getProp = prop => {…}
      ► constructor: class User
      ► __proto__: Object
```
***
### [:briefcase: Упражнения](https://docs.google.com/forms/d/e/1FAIpQLSdQqNcBcLuvW7d7_Msf2a7y1BRbVcUptun6IFQ2ybfqCheTRA/viewform)
***

| [:arrow_double_up:](#es6--ecmascript-2015-) |
|-|
