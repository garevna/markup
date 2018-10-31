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



| [:rewind:](Class#es6--ecmascript-2015-) |
|-|