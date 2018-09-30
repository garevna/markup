# :mortar_board: Объект **`document`**

воспользуемся рекурсивной функцией showProto:
```javascript
function showProto ( elem ) {
    var proto = elem.__proto__
    if ( !proto ) return
    console.info ( proto.constructor.name )
    showProto ( proto )
}
```
для получения цепочки прототипов объекта **`document`**
```javascript
showProto ( document )
```
Результат:
```console
HTMLDocument
Document
Node
EventTarget
Object
```
Объект **`document`** включает две структурные части:

    document.head
    document.body

Если применить функцию **_showProto_** к **`document.head`**:
```javascript
showProto ( document.head )
```
то мы получим такую цепочку протипов:
```console
HTMLHeadElement
HTMLElement
Element
Node
EventTarget
Object
```
Применим функцию **_showProto_** к **`document.body`**:
```javascript
showProto ( document.body )
```
цепочка протипов будет такой:
```console
HTMLBodyElement
HTMLElement
Element
Node
EventTarget
Object
```
| `document` | `document.head` | `document.body` |
|:-:|:-:|:-:|
|  | `HTMLHeadElement` | `HTMLBodyElement` |
| `HTMLDocument` | `HTMLElement` | `HTMLElement` |
| `Document` | `Element` | `Element` |
| `Node` | `Node` | `Node` |
| `EventTarget` | `EventTarget` | `EventTarget` |
| `Object` | `Object` | `Object` |

:warning: `Все цепочки прототипов заканчиваются Object`

:warning: `Все html-элементы наследуют от класса HTMLElement`
***
## :mortar_board:  Свойства объекта **`document`**:

* `✅ document.head      // HTMLHeadElement`
* `✅ document.body      // HTMLBodyElement`
* `✅ document.doctype   // строка`
* `✅ document.URL       // строка`
* `✅ document.location  // объект`
* `✅ document.images    // HTMLCollection`
* `✅ document.forms     // HTMLCollection`
* `✅ document.links     // HTMLCollection`
* `✅ document.scripts   // HTMLCollection`
```javascript
for ( var script of document.scripts )
     console.log ( script.innerText )
```
* `✅ document.styleSheets   // StyleSheetList`
```javascript
for ( var sheet of document.styleSheets ) {
     for ( var rule of sheet.cssRules ) {
          console.warn ( rule.selectorText )
          console.info ( rule.cssText )
     }
}
```
* `✅ document.cookie        // строка`
* `✅ document.lastModified  // строка ( '09/30/2018 11:00:15' )`
...

Выполним код в консоли:
```javascript
for ( var prop in document ) 
    prop.indexOf ( "on" ) === 0 ? 
       console.info ( prop.slice(2) ) : ""
```
Мы получим длинный перечень событий объекта **`document`**

:warning: `Все свойства, имена которых начинаются на "on", могут содержать ссылку на обработчика события, тип которого определяется тем, что следует за "on" в имени свойства`

`по умолчанию эти значениями этих свойств будет null`

:coffee:

`например, присвойте свойству onmouseover объекта document ссылку на функцию:`
```javascript
document.onmouseover = function ( event ) {
    console.info ( `${event.clientX} : ${event.clientY}` )
} 
```
## :mortar_board:  Методы объекта **`document`**:

##### ✅ document.createElement

`Создает элемент DOM и возвращает ссылку на него`

<code>Аргументом метода является строка, содержащая имя тега html-элемента ( `регистр не имеет значения` )</code>

<code>Если переданная строка не соответствует никакому тегу в спецификации языка html, то созданный элемент будет иметь класс **`HTMLUnknownElement`**</code>

:coffee: 1

```javascript
var style = document.createElement ( 'style' )
style.appendChild (
    document.createTextNode (
        `section { border: inset 1px; }`
    )
)
console.log ( style )
```

##### ✅ document.createTextNode

:coffee: 2
```javascript
style.appendChild ( 
    document.createTextNode (
        `div { color: blue; }`
    ) 
)
```
***
Для поиска элементов на странице у объекта **`document`** есть несколько методов:

##### ✅ document.getElementById

<code>ищет элемент по его атрибуту **id**</code>

##### ✅ document.getElementsByTagName
##### ✅ document.getElementsByClassName

<code>Возвращают коллецию html-элементов ( итерабельный объект класса **`HTMLCollection`** ) либо по имени тега, либо по имени класса</code>

##### ✅ document.querySelector

<code>Возвращает первый найденный элемент по указанному селектору</code>

```html
<body>
    <h3 id="demo">demo</h3>
    <section>
        <div title="figure">figure</div>
        <figure class="promoClass">promoClass</figure>
    </section>
    <input type="number">
    <input type="color">
</body>
```

```javascript
document.querySelector ( "section" )
document.querySelector ( "#demo" )
document.querySelector ( ".promoClass" )
document.querySelector ( "[type='number']" )
document.querySelector ( "[title]" )
```

##### ✅ document.querySelectorAll

<code>Возвращает итерабельный объект класса **`NodeList`**, содержащий все элементы, соответствующие указанному селектору</code>
***
[:link: MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document)
***