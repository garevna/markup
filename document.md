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
```javascript
✅ document.head      // __proto__: HTMLHeadElement
✅ document.body      // __proto__: HTMLBodyElement

✅ document.doctype   // строка

✅ document.URL       // строка
✅ document.location  // объект

✅ document.images    // HTMLCollection
✅ document.forms     // HTMLCollection
✅ document.links     // HTMLCollection

✅ document.cookie    // строка
...
```
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

Метод **`createElement`** создает элемент DOM

Аргументом метода является строка, содержащая имя тега html-элемента ( регистр не имеет значения )

Если переданная строка не соответствует никакому тегу в спецификации языка html, то созданный элемент будет иметь класс **_HTMLUnknownElement_**

Для поиска элементов на странице у объекта **`document`** есть несколько методов:

##### ✅ document.getElementById

ищет элемент по его атрибуту **id**

##### ✅ document.getElementsByTagName
##### ✅ document.getElementsByClassName

Возвращают коллецию html-элементов ( итерабельный объект класса **`HTMLCollection`** ) либо по имени тега, либо по имени класса

##### ✅ document.querySelector

Возвращает первый найденный элемент по указанному селектору

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

### ✅ document.querySelectorAll

Возвращает итерабельный объект класса **`NodeList`**, содержащий все элементы, соответствующие указанному селектору
***
## Элементы DOM 

## Свойства элементов DOM 
#### ✅ **`childNodes`**

`Объект` [**`NodeList`**](#nodeType "Типы узлов дерева DOM")

| [:coffee: 1](childNodes-sample-1) |
|-|

[🔗 w3schools](https://www.w3schools.com/jsref/prop_node_childnodes.asp)
***
#### ✅ **`children`**

`Объект` **`HTMLCollection`**

#### ✅ **`lastModified`**

    Строка ( 09/30/2018 11:00:15 )
</code>

## Методы

<a name="nodeType"></a>
### 🎓 Типы узлов дерева DOM

DOM представляет собой граф ( дерево ), вершины которого ( узлы, или **_nodes_** ) могут быть html-элементами, комментариями, обычным текстом...

Получить все дочерние узлы элемента DOM можно с помощью свойства  **`childNodes`**  этого элемента

:coffee: 

```javascript
document.body.childNodes
document.querySelector ( "main" ).childNodes
```
Каждый узел ( объект )  имеет свойство  **_nodeType_**:

| Код | Тип узла | Пример |
|-|-|-|
| `1` | `ELEMENT_NODE` | `<div>` |
| `2` | `ATTRIBUTE_NODE` | `href = "https://translate.google.com/"` |
| `3` | `TEXT_NODE` | `document.body.appendChild ( new Text( "Hello" ) )` |
| `4` | `CDATA_SECTION_NODE` | |
| `5` | `ENTITY_REFERENCE_NODE` | |
| `6` | `ENTITY_NODE` | |
| `7` | `PROCESSING_INSTRUCTION_NODE` | |
| `8` | `COMMENT_NODE` | `<!-- ... -->` |
| `9` | `DOCUMENT_NODE` | `<html>...</html>` |
| `10` | `DOCUMENT_TYPE_NODE` | `<!DOCTYPE>` |
| `11` | `DOCUMENT_FRAGMENT_NODE` | |
| `12` | `NOTATION_NODE` | |

:coffee: 1
```javascript
document.body.appendChild ( new Text( "Hello" ) )
document.body.childNodes
```
```console
▼ NodeList [text]
      0: text
      length: 1
    ► __proto__: NodeList
```
______________________________
https://www.w3schools.com/xml/dom_nodetype.asp