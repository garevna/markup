# :mortar_board: Custom elements
###### Создание кастомных элементов DOM
###### :warning: Имена кастомных тегов обязательно должны состоять минимум из двух частей, разделенных дефисом, например:
```html
<speaking-club></speaking-club>
<gold-prize></gold-prize>
<mystery-man></mystery-man>
```

### HTMLUnknownElement

Если просто вставить на страницу тег с отфанарным именем:
```html
<protuberance></protuberance>
```
то это будет для браузера "НЛО" с непонятным поведением

У такого элемента свойство `__proto__` будет  **_`HTMLUnknownElement`_**

### HTMLElement

При создании класса пользовательских элементов <br/>
в качестве родительского класса ( **super** ) <br/>
можно  использовать HTMLElement

Тогда создаваемый нами элемент будет наследовать свойства и методы родительского класса <br/>
( **_HTMLElement.prototype_** )

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
###### Вставим новый элемент на страницу
```javascript
let elem = document.createElement ( 'sample-element' )
document.body.appendChild ( elem )
```