| [:rewind:](Class#coffee-seven) |
|-|

###### :coffee: :seven:
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

| [:rewind:](Class#coffee-seven) |
|-|