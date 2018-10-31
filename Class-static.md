| [:rewind:](Class) |
|-|

## :mortar_board: static

Статические методы класса объявляются с помощью ключевого слова **static**

Эти методы могут быть вызваны только как методы класса

:warning: Внутри статического метода `this` указывает на конструктор класса, а не на экземпляр

###### :coffee: :one:
```javascript
class Canvas {
    constructor () {
        this.canvas = document.createElement ( 'canvas' )
        document.body.appendChild ( this.canvas )
        Canvas.resizeCanvas.call ( this.canvas )
        this.canvas.style.border = "1px solid #000000"
        this.area = this.canvas.getContext ( "2d" )
    }
    static resizeCanvas ( event ) {
        this.width = window.innerWidth - 30
        this.height = window.innerHeight - 20
    }
    static drawLine ( context, points ) {
        context.area.moveTo( points[0].x, points[0].y )
        context.area.lineTo( points[1].x, points[1].y )
        context.area.stroke()
    }
}

let pict = new Canvas ()
window.onresize = Canvas.resizeCanvas.bind ( pict.canvas )
Canvas.drawLine ( pict, [ { x: 50, y: 50 }, { x: 250, y: 250 } ] )
Canvas.drawLine ( pict, [ { x: 250, y: 250 }, { x: 100, y: 250 } ] )
```
✋ Обратите внимание, что статические методы **_resizeCanvas_** и **_drawLine_** <br/>
вызываются как методы класса **Canvas**:
```javascript
Canvas.resizeCanvas
Canvas.drawLine
```
✋ Внутри конструктора  `this`  указывает  на экземпляр

В этом примере для того, чтобы внутри метода `this` указывал на объект **canvas** экземпляра, <br/>
вызов метода  **_resizeCanvas_** из конструктора происходит с передачей контекста:
```javascript
Canvas.resizeCanvas.call ( this.canvas )
```
и когда этот метод используется в качестве обработчика события **_resize_** объекта  **`window`**, <br/>
то выполняется явная привязка контекста:
```javascript
window.onresize = Canvas.resizeCanvas.bind ( pict.canvas )
```
При вызове статического метода  **_drawLine_**  первым аргументом ему передается контекст вызова

> ✍ Примечание: 
 
> В данном случае объявление метода  drawLine  как статического <br/>
> создает ненужные сложности с передачей контекста, <br/>
> и гораздо проще объявить его так:
```javascript
drawLine ( points ) {
    this.area.moveTo( points[0].x, points[0].y )
    this.area.lineTo( points[1].x, points[1].y )
    this.area.stroke()
}
```
> чтобы контекстом вызова был экземпляр, создаваемый конструктором

| [:rewind:](Class) |
|-|

***
###### :coffee: :two:
```javascript
class Canvas {
    constructor () {
        this.canvas = document.createElement ( 'canvas' )
        document.body.appendChild ( this.canvas )
        Canvas.resizeCanvas ()
    }
    static resizeCanvas ( event ) {
        console.log ( `name: "${this.name}"` )
    }
}

var pict = new Canvas ()
window.onresize = Canvas.resizeCanvas
```
Когда метод **_resizeCanvas()_** будет вызван из конструктора, он выведет в консоль:
```
name: "Canvas"
```
Измените размер окна браузера<br/>
Теперь метод  **_resizeCanvas()_**  будет вызван в глобальной области видимости,<br/>
и в консоль будет выведено:
```
name: ""
```
поскольку  `this`  внутри **_resizeCanvas()_** теперь указывает
на глобальный объект  ( `window` )

| [:rewind:](Class) |
|-|