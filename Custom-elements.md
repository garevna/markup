# :mortar_board: Custom elements
###### Создание кастомных элементов DOM
###### :warning: Имена кастомных тегов обязательно должны состоять минимум из двух частей, разделенных дефисом, например:
```html
<speaking-club></speaking-club>
<gold-prize></gold-prize>
<mystery-man></mystery-man>
```

### :squirrel: HTMLUnknownElement

###### Если просто вставить на страницу тег с отфанарным именем:
```html
<protuberance></protuberance>
```
###### то свойство `__proto__` такого элемента будет  **_`HTMLUnknownElement`_**
```javascript
console.dir ( document.querySelector ( 'protuberance' ).__proto__ )
```
```console
► HTMLUnknownElement
```
###### А вот прототипом **_`HTMLUnknownElement`_** будет уже известный нам **`HTMLElement`**
```javascript
console.dir ( HTMLUnknownElement )
```
```console
ƒ HTMLUnknownElement()
    arguments: null
    caller: null
    length: 0
    name: "HTMLUnknownElement"
    prototype: HTMLUnknownElement {constructor: ƒ, Symbol(Symbol.toStringTag): "HTMLUnknownElement"}
    __proto__: ƒ HTMLElement()
```
###### Поэтому элемент _protuberance_ унаследует все свойства и методы, которые мы обнаружим в свойстве `prototype` конструктора _HTMLElement_

`Однако никаких "специфических" свойств и методов у этого элемента не будет, что полностью нивелирует "ценность" подобного творения`

###### :warning: При создании класса пользовательских элементов в качестве родительского класса ( **super** ) можно  использовать HTMLElement
###### Тогда создаваемый нами элемент будет наследовать свойства и методы родительского класса _HTMLElement.prototype_

## customElements

Свойство **`customElements`** ( _read-only_ ) глобального объекта `Window` содержит ссылку на объект **`CustomElementRegistry`**

```javascript
console.dir ( customElements )
```
```console
▼ CustomElementRegistry
  ▼ __proto__: CustomElementRegistry
      ► define: ƒ define()
      ► get: ƒ ()
      ► upgrade: ƒ upgrade()
      ► whenDefined: ƒ whenDefined()
      ► constructor: ƒ CustomElementRegistry()
        Symbol(Symbol.toStringTag): "CustomElementRegistry"
      ► __proto__: Object
```
###### Можно посмотреть, чьим "наследником" является **`customElements`**

```javascript
console.dir ( CustomElementRegistry )
```
```console
▼ ƒ CustomElementRegistry()
    arguments: null
    caller: null
    length: 0
    name: "CustomElementRegistry"
  ▼ prototype: CustomElementRegistry
      ► define: ƒ define()
      ► get: ƒ ()
      ► upgrade: ƒ upgrade()
      ► whenDefined: ƒ whenDefined()
      ► constructor: ƒ CustomElementRegistry()
        Symbol(Symbol.toStringTag): "CustomElementRegistry"
      ► __proto__: Object
  ► __proto__: ƒ ()
```
Мы будем использовать **`CustomElementRegistry`** для регистрации собственных ( кастомных ) элементов <br/>
а так же для получения информации об уже зарегистрированных элементах

### customElements.define ()

Метод  **`define()`** глобального объекта **customElements** имеет два обязательных параметра:

* первый - это имя тега для регистрируемого элемента
* второй - ссылка на класс создаваемого элемента
```javascript
customElements.define (
    'sample-custom-element', 
    SampleCustomElement 
)
```
***
:coffee: :one:
###### Объявим класс SampleElement, расширяющий класс HTMLElement
```javascript
class SampleElement extends HTMLElement {
    constructor() {
        super ()
        let wrapper = document.createElement ( 'div' )
        wrapper.className = "wrapper"
        this.picture = document.createElement ( 'img' )
        this.setPicture ( "https://images.pexels.com/photos/33044/sunflower-sun-summer-yellow.jpg" )
        wrapper.appendChild ( this.picture )
        this.picture.angle = 0
        this.button = document.createElement ( 'button' )
        this.button.innerText = 'ROTATE'
        this.button.onclick = this.rotatePicture.bind ( this )
        wrapper.appendChild ( this.button )

        let style = document.createElement ( 'style' )
        style.textContent = `
            .wrapper {
                background-color: #ddddee;
            }
            img {
                width:200px;
                margin: 20%;
                border: dotted 1px #555;
                transition: all 1s;
            }
        `

        this.shadow = this.attachShadow ( { mode: 'open' } )
        this.shadow.appendChild ( style )
        this.shadow.appendChild ( wrapper )
    }
    setPicture ( url ) {
        this.picture.src = url
    }
    rotatePicture () {
        this.picture.angle += this.picture.angle < 270 ? 90 : -270
        this.picture.style.transform = `rotate(${this.picture.angle}deg)`
    }
}
```
###### Зарегистрируем новый элемент класса _SampleElement_
```javascript
customElements.define ( 'sample-element', SampleElement )
```
###### Проверим, был ли зарегистрирован наш элемент в `CustomElementRegistry`
```javascript
customElements.get ( 'sample-element' )
```
```console
class SampleElement extends HTMLElement {
    constructor() {
        super ()
        let wrapper = document.createElement ( 'div' )
        wrapper.className = "wrapper"
        this.picture = document.c…
```
###### Вставим новый элемент на страницу
```javascript
let elem = document.createElement ( 'sample-element' )
document.body.appendChild ( elem )
```
***
:coffee: :two:
```javascript
class SampleCustomElement extends HTMLElement {
    constructor () {
        super ()
        let wrapper = document.createElement ( 'div' )
        wrapper.className = "wrapper"
        this.canvas = document.createElement ( 'canvas' )
        wrapper.appendChild ( this.canvas )
        this.resizeCanvas ()
        this.area = this.canvas.getContext ( "2d" )
        this.shadow = this.attachShadow ( { mode: 'open' } )
        let style = document.createElement ( 'style' )
        style.textContent = `
            .wrapper {
                background-color: #ddddee;
            }
            canvas {
                border: dotted 1px #555;
            }
        `
        this.shadow.appendChild ( style )
        this.shadow.appendChild ( wrapper )
    }
    resizeCanvas ( event ) {
        this.canvas.width = window.innerWidth - 20
        this.canvas.height = window.innerHeight - 20
    }
    drawLine ( first, second, border ) {
        this.area.strokeStyle = border && border.lineColor ? 
                                border.lineColor : "#0000ff"
        this.area.lineWidth = border && border.lineWidth ? 
                              border.lineWidth : 3
        this.area.beginPath()
        this.area.moveTo( first.x, first.y )
        this.area.lineTo( second.x, second.y )
        this.area.stroke()
    }
}

customElements.define (
    'sample-custom-element', 
    SampleCustomElement 
)

let elem = document.createElement ( 'sample-custom-element' )
document.body.appendChild ( elem )

window.onresize = elem.resizeCanvas.bind ( elem )

elem.drawLine (
    { x:20, y:20 },
    { x:400, y:200 },
    { lineColor: "#008595", lineWidth: 5 } 
)
```
***
:coffee: :three:
```html
<h3>Пример использования Custom Elements</h3>
<article contenteditable = true>
   <p>Статические методы класса объявляются с помощью ключевого слова <b>static</b></p>
   <p>Эти методы недоступны из экземпляров класса</p>
   <p>Они могут быть вызваны только как методы класса</p>
   <words-counter></words-counter>
</article>
```
```javascript
class WordsCounter extends HTMLElement {
    constructor () {
        super()
        let textContainer = this.parentNode
        let shadow = this.attachShadow ( { mode: 'open' } )
        let style = document.createElement ( 'style' )
        style.textContent = `
            span {
                background-color: #ddddee;
                display: inline-block;
                padding: 5px 10px;
                color: #578;
                border: "1px solid #578";
            }
        `
        shadow.appendChild ( style )
        function countWords ( node ) {
            var text = node.innerText || node.textContent
            return text.split(/\s+/g).length
        }
        let counter = `Words: ${countWords(textContainer)}`
        let counterElem = document.createElement ('span')
        counterElem.textContent = counter
        shadow.appendChild ( counterElem )
        setInterval ( function () {
            var counter = `Words: ${countWords(textContainer)}`
            counterElem.textContent = counter
        }, 200 )
    }
}
customElements.define (
    'words-counter',
    WordsCounter
)
```
***
:coffee: :four:
```javascript
class SampleCustomElement extends HTMLElement {
    constructor () {
        super ()
        let wrapper = document.createElement ( 'div' )
        wrapper.className = "wrapper"
        this.canvas = document.createElement ( 'canvas' )
        wrapper.appendChild ( this.canvas )
        this.resizeCanvas ()
        this.area = this.canvas.getContext ( "2d" )
        this.canvas.self = this
        this.canvas.history = []
        this.canvas.onmousemove = function ( event ) {
            let point = { x: event.clientX, y: event.clientY }
            this.self.drawLine ( 
                point, 
                { lineColor: "#f0f", lineWidth: 3 } )
        }
        this.shadow = this.attachShadow ( { mode: 'open' } )
        let style = document.createElement ( 'style' )
        style.textContent = `
            .wrapper {
                background-color: #ddddee;
            }
            canvas {
                border: dotted 1px #555;
            }
        `
        this.shadow.appendChild ( style )
        this.shadow.appendChild ( wrapper )
    }
    resizeCanvas ( event ) {
        this.canvas.width = window.innerWidth - 20
        this.canvas.height = window.innerHeight - 20
    }
    drawLine ( point, border ) {
        if ( !point || !point.x || !point.y ) return
        this.canvas.history.push ( point )
        let len = this.canvas.history.length
        if ( len < 2 )  return
        let prev = this.canvas.history [ len - 2 ] 
        this.area.strokeStyle = border && border.lineColor ? 
                                border.lineColor : "#0000ff"
        this.area.lineWidth = border && border.lineWidth ? 
                              border.lineWidth : 3
        this.area.beginPath()
        this.area.moveTo( prev.x, prev.y )
        this.area.lineTo( point.x, point.y )
        this.area.stroke()
    }
}

customElements.define (
    'sample-custom-element', 
    SampleCustomElement 
)

let elem = document.createElement (
    'sample-custom-element'
)
document.body.appendChild ( elem )

window.onresize = elem.resizeCanvas.bind ( elem )
```