| [:rewind:](Class#es6--ecmascript-2015-) |
|-|

###### Наследование
### super
Методы родительского класса доступны в дочернем классе посредством ключевого слова **`super`**

Расширим метод **drawLine**  родительского класса, добавив аргумент **_lineWidth_**  ( толщину линии )

Для этого определим "расширенный" метод  **drawLine** внутри дочернего класса,<br/>
который будет вызывать  метод  **drawLine**  родительского класса<br/>
с помощью ключевого слова super:
```javascript
super.drawLine ( points, lineColor )
```
Теперь код будет таким:
```javascript
const Canvas = class {
    constructor () {
        this.canvas = document.createElement ( 'canvas' )
        document.body.appendChild ( this.canvas )
        this.canvas.style.border = "1px solid #000000"
        this.area = this.canvas.getContext ( "2d" )
    }
    drawLine ( points ) {
        this.area.beginPath()
        this.area.moveTo( points[0].x, points[0].y )
        this.area.lineTo( points[1].x, points[1].y )
        this.area.stroke()
    }
}

class ExtendedCanvas extends Canvas {
    drawLine ( points, lineColor, lineWidth ) {
        this.area.lineWidth = lineWidth || 3
        this.area.strokeStyle = lineColor
        super.drawLine ( points )
    }
}
```
Создадим экземпляр дочернего класса:
```javascript
let newCanvas = new ExtendedCanvas ()
```
и вызовем его метод  **drawLine**
```javascript
newCanvas.drawLine (  [ { x: 20, y: 20 }, { x: 300, y: 400 } ], "#ffaa00", 10 )
```
Теперь линия будет отрисовываться заданной толщины

***

### super ()

В предыдущих примерах мы не использовали конструктор наследующего класса

    ☝ Когда нужно добавить свойства 
     экземпляру наследующего класса,
     без конструктора это сделать невозможно

✋ Первое, что нужно выполнить в конструкторе наследующего класса - 
      вызвать метод  **super ()**
```javascript
const Canvas = class {
    constructor () {
        this.canvas = document.createElement ( 'canvas' )
        document.body.appendChild ( this.canvas )
        this.area = this.canvas.getContext ( "2d" )
    }
    drawLine ( points ) {
        this.area.beginPath()
        this.area.moveTo( points[0].x, points[0].y )
        this.area.lineTo( points[1].x, points[1].y )
        this.area.stroke()
    }
}

class ExtendedCanvas extends Canvas {
    constructor () {
        super ()
        this.history = []
    }
}
```
В противном случае будет сгенерировано исключение:
```
⛔️ Uncaught ReferenceError: 
Must call super constructor in derived class before accessing 'this' or returning from derived constructor
```

### super в литералах объектов

Ключевое слово  `super`  можно использовать без объявления классов<br/>
Он является просто ссылкой на прототип объекта<br/>
Поэтому можно использовать его для доступа к свойствам и методам объекта-прототипа

В примерах далее мы будем использовать объекты, объявленные в литеральной форме<br/>
В качестве прототипа объекта  **person**  будет выступать объект  **human**<br/>
Назначать объект  **human**  прототипом объекта  **person** мы будем с помощью метода
```javascript
Object.setPrototypeOf ( person, human )
```
После такого назначения внутри объекта  **person**  <br/>
свойства и методы объекта  **human** будут доступны <br/>
с помощью ключевого слова  **`super`**

В следующем примере вызовем методы  **_place ()_**  и  **_say ()_**  <br/>
прототипа **human**  <br/>
в методах   **_getPlace ()_**  и  **_talk ()_**  <br/>
объекта  **person**  <br/>
с помощью ключевого слова **`super`** :

###### :coffee: :one:
```javascript
let human = {
    place () {
        var x = document.createElement ( "p" )
        document.body.appendChild ( x )
        x.id = "demo"
        return x
    },
    say ( text ) {
        this.place.innerHTML = text
    }
}

let person = {
    getPlace () { this.place = super.place () },
    talk ( text ) {
        super.say ( text )
    }
}

Object.setPrototypeOf ( person, human )
person.getPlace ()
person.talk ( "привет!" )
```
###### :coffee: :two:

✍ В этом примере метод  **_place()_**  прототипа  ( объекта  **human** ) <br/>
проверяет наличие элемента с  `id === "demo"`,  <br/>
и если такой элемент найден, <br/>
возвращает ссылку на него, <br/>
в противном случае создает такой элемент, <br/>
добавляет его на страницу и возвращает ссылку на него

✍ Объект  person  изначально не имеет свойства  **_place_**, <br/>
но имеет собственный метод  **_getPlace ()_**,  <br/>
который создает такое свойство,  <br/>
вызывая с помощью ключевого слова  **`super`**  <br/>
метод   **_place()_**  прототипа  ( объекта  **human** ), <br/>
и присваивая возвращенное этим методом <br/>
значение собственному свойству  **_place_**

✍ Метод  **_talk( `text` )_**  объекта  **person**  <br/>
вызывает метод  **_getPlace()_**<br/>
до вызова метода **_say ()_**  <br/>
прототипа  ( объекта  **human** )

```javascript
let human = {
    place: () => 
        document.getElementById ( "demo" ) ? 
        document.getElementById ( "demo" ) :
        document.body.appendChild ( 
            document.createElement ( "p" ) 
        ).id = "demo",

    say ( text ) {
        this.place.innerHTML = text
    }
}

let person = {
    getPlace () { this.place = super.place() },
    talk ( text ) {
        this.getPlace ()
        super.say ( text )
    }
}

Object.setPrototypeOf ( person, human )

person.talk ( "привет!" )
setTimeout ( () => person.talk ( "Hello, baby!" ), 2000 )
```

☝ Обратите внимание, <br/>
что при объявлении метода   **_place()_**  объекта  **human**  <br/>
мы использовали стрелочную функцию, <br/>
а при объявлении метода  say  ее использовать нельзя, <br/>
поскольку внутри методов, <br/>
объявленных с помощью стрелочных функций,  <br/>
контектом вызова будет глобальный объект  window


| [:rewind:](Class#es6--ecmascript-2015-) |
|-|