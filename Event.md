# :mortar_board: Events

В цепочке прототипов любого элемента DOM есть объект ( класс ) **`EventTarget`**

Благодаря этому все элементы DOM способны "реагировать" на события

Выведем в консоль этот объект:

```javascript
console.dir ( EventTarget )
```
Более всего нас интересует, конечно, его свойство **_`prototype`_**
```console
▼ ƒ EventTarget()
    arguments: null
    caller: null
    length: 0
    name: "EventTarget"
    ▼ prototype: EventTarget
        ► addEventListener: ƒ addEventListener()
        ► dispatchEvent: ƒ dispatchEvent()
        ► removeEventListener: ƒ removeEventListener()
        ► constructor: ƒ EventTarget()
          Symbol(Symbol.toStringTag): "EventTarget"
        ► __proto__: Object
    ► __proto__: ƒ ()
```
Здесь мы видим три метода, которые унаследуют все объекты, имеющие в цепочке прототипов  **`EventTarget`**

Мы уже в курсе, что объект **`Node`** наследует от объекта **`EventTarget`**, 

а объект **`Element`** наследует от **`Node`**,

потому что элементы DOM - это частный случай узла DOM

В свойстве **_`prototype`_** объекта **`Element`** мы обнаружим не слишком длинный перечень свойств, начинающихся на **_`on`_**

Однако объект **`Element`** является только прототипом объекта **`HTMLElement`**

А вот последний как раз и является непосредственным прототипом всех элементов DOM

Поэтому, очевидно, искать события, общие для всех элементов DOM, нужно именно в его свойстве **_`prototype`_**

```javascript
for ( var prop in HTMLElement.prototype ) {
    if ( prop.indexOf ( 'on' ) !== 0 ) continue
    console.info ( `Event: ${prop.slice(2)}` ) 
}
```
Однако элементы DOM значительно отличаются друг от друга

У каждого html-элемента есть собственный конструктор, который "добавляет" специфические" для этого элемента события

( например, события **`input`** и **`change`** могут произойти только на элементах форм )
***
:warning: Событие - это объект 😉

каждое событие создается конструктором **`Event`**

У каждого события есть свойство  **_`type`_** ( строка ):

    ✅ click
    ✅ mouseover
    ✅ mouseout
    ✅ mouseenter
    ✅ mouseleave
    ✅ mousedown
    ✅ mouseup
    ✅ keydown
    ✅ keyup
    ...
***
Полный перечень событий DOM можно найти в спецификации:

[:link: :one:](https://www.w3schools.com/jsref/dom_obj_event.asp)
[:link: :two:](https://www.w3schools.com/js/js_events.asp)
***

## :mortar_board: host-объект Event

Конструктор, с помощью которого создаются все события DOM

Свойство  **_`prototype`_**  конструктора **`Event`** содержит свойства, которые будут унаследованы всеми событиями 
***


:coffee: 1
```javascript
function addElement ( tagName, container ) {
    var _container = 
        container && container.nodeType === 1 ? 
                    container : document.body
    return _container.appendChild (
         document.createElement ( tagName )
    )
}

var obj = addElement ( "h1" )

obj.innerText = "Hi"

obj.addEventListener ( "listen", listenHandler )

function listenHandler ( event ) {
    this.innerText = event.detail
}

var btn = addElement ( "button" )
btn.innerText = "Change"

btn.onclick = function ( event ) {
    var inp = addElement ( "input" )
    inp.onchange = function ( event ) {
        obj.dispatchEvent ( 
             new CustomEvent ( "listen",
                  { 
                       detail: this.value
                  } 
             ) 
        )
        this.parentNode.removeChild ( this )
    }
}
```

### [:briefcase: Упражнения](https://docs.google.com/forms/d/e/1FAIpQLSdeCCJVXykUJdr9gIroRT1H4K2JD6bhSreAs_tvsLd9vaNReQ/viewform)