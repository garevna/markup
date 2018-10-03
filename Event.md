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

* [addEventListener](#addEventListener)
* [removeEventListener](#removeEventListener)
* [dispatchEvent](#dispatchEvent)

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
```javascript
var userEvent = new Event( 'user' )
```
## :mortar_board: dispatchEvent

Метод dispatchEvent "отправляет" событие элементу

```javascript
document.body.onclick = function ( event ) {
    this.style.backgroundColor = "#fa0"
}
document.body.dispatchEvent ( new Event ( 'click' ) )
```

## :mortar_board: CustomEvent

Конструктор CustomEvent создает кастомное событие c дополнительными параметрами

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
***
## :mortar_board: event handler

У всех элементов есть свойства с именами, начинающимися с  "**on**"

Значения этих свойств должны быть ссылкой на функцию, которая будет вызвана при возникновении события ( *event handler* )

Обработчик события - это функция, которая вызывается тогда, когда событие произошло

Если определить значение свойства  **_`onclick`_**  элемента как функцию **_clickCallback_**, то в момент, когда пользователь кликнет левой кнопкой мышки на этом элементе, будет вызвана функция **_clickCallback_**

Функция  **_clickCallback_** станет обработчиком события  **`click`**  элемента

:warning: Обработчики события в момент их вызова получают в качестве первого аргумента **объект события**

`Поэтому при объявлении функции-обработчика настоятельно рекомендуется в качестве первого параметра указывать имя переменной, в которую будет помещена ссылка на объект события:`
```javascript
elem.onclick = function ( event ) { ... }
elem.onmouseover = function ( mev ) { ... }
```
Таким образом объект события становится доступным внутри обработчика

#### :mortar_board: event.screenX | event.screenY
Координаты указателя мышки относительно левого верхнего угла физического экрана 

#### :mortar_board: event.clientX | event.clientY
Координаты указателя мышки относительно верхнего левого края видимой части окна браузера ( **_viewport_** )

| [:coffee:](https://codepen.io/garevna/pen/jLbaMg) |
|-|

Эти координаты не зависят от положения полосы прокрутки окна браузера

#### :mortar_board: event.pageX | event.pageY

Координаты указателя мышки относительно верхнего левого края страницы

Эти координаты зависят от положения полосы прокрутки окна браузера

#### :mortar_board: eventPhase

| [:coffee:](https://jsfiddle.net/garevna/1cL6nk8j/4/) |
|-|

## :mortar_board: eventListener

Методы добавления и удаления прослушивателей событий:

✅ addEventListener

✅ removeEventListener

👀 Свойства "on..." позволяют "повесить" только одного обработчика данного события на данный элемент

👂 eventListener-ов может быть сколько угодно для одного и того же элемента и одного и того же события

Предположим, мы вешаем обработчика события mousemove на все элементы **div**

Затем вешаем "персонального" обработчика события **_`mousemove`_** на  **`div#sample`**

На  элементе  **`div#sample`**  "сработают" оба обработчика при наведении указателя мышки

<a name="addEventListener"></a>
### :mortar_board: addEventListener

Первый аргумент метода addEventListener - это тип события ( строка ), например:
        "mouseover"
        "mouseout"
        "input"
        "change"
        ...

Второй аргумент - ссылка на функцию ( обработчика события )

:coffee: :one:
```javascript
document.getElementById ( '#sample' )
    .addEventListener ( 'click', function ( event ) {
         console.log ( 'sample click event: ', event )
     })
```
:coffee: :two:
```javascript
var elem = document.body.appendChild (
    document.createElement ( "p" )
)
elem.innerText = "Hello"
function clickdHandler ( event ) {
    this.innerHTML = `
        <small>
            My content was changed!
        </small>
    `
}
elem.addEventListener ( 'click', clickdHandler )
```
Третий аргумент - логическое значение - будучи установленным в **`true`**, позволяет перехватить событие на фазу погружения ( **_capturing_** )

:coffee: :three:
```javascript
var btn = document.createElement ( 'button' )
btn.innerText = "OK"
btn.style = `
    background-image: url(https://cdn2.iconfinder.com/data/icons/user-23/512/User_Yuppie_2.png);
    background-size: contain;
    background-repeat: no-repeat;
    background-position: left center;
    padding: 5px 10px 5px 30px;
`
document.body.appendChild ( btn )

btn.addEventListener ( 'click', function ( event ) {
    console.log ( event.currentTarget.tagName, event.eventPhase )
}, true )

document.body.addEventListener ( 'click', function ( event ) {
    console.info ( event.currentTarget.tagName, event.eventPhase )
}, true )
```

<a name="removeEventListener"></a>
### :mortar_board: removeEventListener

Прослушивателей событий нужно удалять, поскольку они не убираются автоматически при удалении элемента

При удалении нужно передавать точно такие же аргументы, какие были переданы методу addEventListener при создании прослушивателя

:coffee: :four:

Такой вариант удаления не сработает:
```javascript
document.getElementById ( 'sample' )
    .addEventListener ( 'click', function ( event ) {
         console.log ( 'sample click event: ', event )
     })
document.getElementById ( 'sample' )
    .removeEventListener ( 'click', function ( event ) {
         console.log ( 'sample click event: ', event )
    })
```
:coffee: :five:

А такой - да:
```javascript
function clickHandler ( event ) {
   this.innerHTML = '<small>My content was changed!</small>'
}
elem.addEventListener ( 'click', clickHandler )
elem.removeEventListener ( 'click', clickHandler )
```
:coffee: :six:
```html
<div id="main-frame" class="wrapper">
    <div id="main-content">
        <div id="main-message">
            <h1>Event Listener</h1>
            <p>Тестируем работу eventListener</p>
            <div id="list">
               <p>Что нужно помнить:</p>
               <ul class="single">
                  <li>eventListener-ов нужно удалять</li>
                  <li>Для этого есть метод removeEventListener</li>
               </ul>
           </div>
           <div class="error">Error was detected</div>
           <div id="diagnose">Печалька</div>
        </div>
    </div>
</div>
<div id="error">
   <p id="details">____________________</p>
</div>
```
```javascript
var collection = document.querySelectorAll ( 'p ~ *' )
collection.forEach ( x => {
   if ( x.nodeType === 1 )
       x.addEventListener ( 'mouseover', function ( event ) {
           console.warn ( 
              event.target.tagName + (
              event.target.id ? '#' + event.target.id : 
              event.target.className ?
              '.' + event.target.className :
              ' content: ' + event.target.innerHTML )
           )
      } )
} )

var elem = document.querySelector ( '#list' )
elem.addEventListener ( 'mouseover', function ( event ) {
   event.target.innerHTML = `event: ${new Date().toLocaleString()}`
} )

function clickHandler ( event ) {
   this.innerHTML = '<small>My content was changed!</small>'
}
elem.addEventListener ( 'click', clickHandler )
```

### :mortar_board: preventDefault()

Иногда мы не хотим, чтобы при наступлении события элемент HTML вел себя так, как он должен себя вести по умолчанию

В таком случае мы можем использовать метод **`preventDefault()`**

Например, по умолчанию в результате клика на гиперссылке происходит переход по адресу, указанному атрибутом *href*

Мы можем внутри обработчика события **_`click`_** элемента **`a`** вызвать метод **_`preventDefault()`_**, что предотвратит поведение по умолчанию, и перехода не будет

:coffee: :seven:
```javascript
var elem = document.body.appendChild ( 
     document.createElement ( 'a' )
)
elem.innerText = "click me"
elem.href = "https://www.w3schools.com/charsets/ref_utf_punctuation.asp"
elem.addEventListener ( 'click', 
    function ( event ) {
        event.preventDefault()
        alert ( `href: ${this.href}` )
    }
)
```
### :mortar_board: stopPropagation()

Почти все события "всплывают" ( но не все, например, событие *_focus_* не всплывает )

Предотвращает "всплытие" события, т.е. срабатывание обработчиков этого события на элементах, внутри которых находится целевой элемент

:coffee: :eight:

Запустите код в консоли, кликните на самом маленьком кружке и посмотрите, что будет выведено в консоль

```javascript
var elemData = {
   name: "div",
    attrs: {
       className: "container",
       title: "Контейнер",
       style: `
           position: absolute;
           top: 20px;
           left: 20px;
           border-radius: 50%;
           border: dotted 2px #789;
           background-color: #70ff9090;
       `
   }
}
function clickHandler ( event ) {
    // event.stopPropagation()
    console.info ( this.num )
}

function insertElement ( elemNum, parentElem ) {
   var elem = parentElem.appendChild (
       document.createElement ( elemData.name )
   )
   elem.num = elemNum

   for ( var attr in elemData.attrs )  
      elem [ attr ] = elemData.attrs [ attr ]
   elem.style.width = `${400 - elemNum * 50}px`
   elem.style.height = `${400 - elemNum * 50}px`

   elem.addEventListener ( 'click', clickHandler )
   return elem
}

var elems = []
elems [0] = insertElement ( 0, document.body )
for ( var x = 1; x < 5; x++ ) {
   elems [x] = insertElement ( x, elems [ x - 1 ] )
}
```
Теперь перезагрузите страницу, опять вставьте код, но раскомментируйте строку   
```javascript
event.stopPropagation()
```
кликните на самом маленьком кружке и посмотрите, что будет выведено в консоль

### :mortar_board: stopImmediatePropagation()

Если у элемента есть несколько прослушивателей одного и того же события, они будут вызваны в том порядке, в котором они были добавлены

Если один из обработчиков, установленных одним из этих listener-ов, вызовет метод **`event.stopImmediatePropagation ()`**, то остальные listener-ы, следующие за ним, уже не сработают

:coffee: :nine:

Если выполнить следующий код в консоли:
```javascript
var elem = document.body.appendChild (
    document.createElement ( 'p' )
)
elem.innerHTML = 'Click me, please'

var text = [
    'Hello',
    'are you happy?',
    'what is your favorite language?',
    'Bye'
]
elem.addEventListener ( 'click', 
   function ( event ) {
      // event.stopImmediatePropagation()
      console.log ( 'Я тут первый, остальные на фиг!' )
   }
)
for ( var txt of text ) {
    elem.addEventListener ( 'click', 
        ( function ( message ) {
            return function () {
                console.log ( message )
            }
        })( txt )
    )
}
```
то при клике на элементе сработают все прослушиватели собятия click элемента в той последовательности, в какой мы их определили

Однако если убрать слеши перед строчкой
```javascript
event.stopImmediatePropagation()
```
то сработает только один прослушиватель, и выведена в консоль будет только одна строчка
***
🔗 https://www.w3schools.com/js/js_htmldom_eventlistener.asp

***
Примеры в песочнице:

[:coffee: mouseover & mouseout](https://codepen.io/garevna/pen/jLrReP?editors=1010)

[:coffee: mouseover & mouseout vs mouseenter & mouseleave](https://codepen.io/garevna/pen/gxaOXq)

[:coffee: onscroll | onwheel](https://jsfiddle.net/garevna/ayoLy5eL/1/)

[:coffee: keypress vs keydown](https://codepen.io/garevna/pen/PKPQVR)

<a name="dispatchEvent"></a>
[:coffee: dispatchEvent](https://codepen.io/garevna/pen/gxpQvy)

***
### [:briefcase: Упражнения](https://docs.google.com/forms/d/e/1FAIpQLSdeCCJVXykUJdr9gIroRT1H4K2JD6bhSreAs_tvsLd9vaNReQ/viewform)