# :mortar_board: Shadow DOM
<code>
До появления Shadow DOM инкапсуляция стилей элементов DOM была острой проблемой разработчиков

Однако с учетом поддержки Shadow DOM всеми основными браузерами эта проблема больше не существует
</code>

**Shadow DOM** - это суверенное дерево DOM-узлов элемента

**`Shadow DOM API`**  обеспечивает возможность привязать **Shadow DOM** к отдельному элементу

###### Термины:
<h6>
:small_blue_diamond: <em>Shadow host</em> - элемент DOM, к которому привязан shadow DOM<br/>
:small_blue_diamond: <em>Shadow tree</em> - дерево элементов DOM внутри shadow DOM<br/>
:small_blue_diamond: <em>Shadow boundary</em> - граница между shadow DOM и обычным DOM<br/>
:small_blue_diamond: <em>Shadow root</em> - корневой элемент дерева shadow DOM<br/>
</h6>

Оперировать элементами shadow DOM можно точно так же, как и обычными DOM элементами:

<h6>можно добавлять дочерние элементы или атрибуты настройки,<br/>
стилизовывать отдельные узлы с помощью element.style<br/>
или применять стили ко всему дереву shadow DOM внутри элемента <style>
</h6>

Преимущество заключается в том, что содержимое shadow DOM инкапсулировано внутри него, и не может отразиться на поведении или стилях других элементов DOM

Кроме того, все свойства элемента, "спрятанные"  в  его shadow DOM, не могут быть случайно изменены извне
***
## :mortar_board: attachShadow ()

Добавить элементу его собственный shadow DOM очень легко<br/>
Для этого существует метод **`attachShadow()`**<br/>
Метод  **`attachShadow()`**  принимает в качестве аргумента объект опций, который содержит единственную опцию **`mode`**<br/>
Опция  **`mode`**  может иметь значение  **_`'open'`_**  или  **_`'closed'`_**
```javascript
var elem = document.createElement ( 'div' )
elem.attachShadow ( { mode: 'open' } )
```
:coffee: :one:
```javascript
let elem = document.createElement ( 'div' )
document.body.appendChild ( elem )
let shadow = elem.attachShadow ( { mode: 'open' } )
shadow.appendChild (
    ( () => {
        var script = document.createElement ( 'script' )
        script.innerText = `console.log ( "HELLO!" )`
        return script
    })()
)
shadow.appendChild (
    ( () => {
        var pict = document.createElement ( 'img' )
        pict.src = "http://www.radioactiva.cl/wp-content/uploads/2018/05/pikachu.jpg"
        return pict
    })()
)
shadow.appendChild (
    ( () => {
        var style = document.createElement ( 'style' )
        style.textContent = 'img { width: 200px; }'
        return style
    })()
)
```

#### mode: 'open'
Значение  **_'open'_**  означает, что `shadow DOM`  данного элемента будет доступен в контексте страницы через его свойство **`shadowRoot`**
```html
▼ <div>
  ▼ #shadow-root ( open )
       <img src="http://www.radioactiva.cl/wp-content/uploads/2018/05/pikachu.jpg">
       <style>img { width: 200px; }</style>
</div>
```
###### Доступные свойства shadowRoot
```javascript
console.dir ( elem.shadowRoot )
```
```console
▼ #document-fragment
    activeElement: null
    baseURI: "about:blank"
    childElementCount: 2
  ► childNodes: NodeList(2) [img, style]
  ► children: HTMLCollection(2) [img, style]
    delegatesFocus: false
  ► firstChild: img
  ► firstElementChild: img
  ► host: div
    innerHTML: "<img src="http://www.radioactiva.cl/wp-content/uploads/2018/05/pikachu.jpg"><style>img { width: 200px; } 
    </style>"
    isConnected: true
  ► lastChild: style
  ► lastElementChild: style
    mode: "open"
    nextSibling: null
    nodeName: "#document-fragment"
    nodeType: 11
    nodeValue: null
  ► ownerDocument: document
    parentElement: null
    parentNode: null
    pictureInPictureElement: null
    pointerLockElement: null
    previousSibling: null
  ► styleSheets: StyleSheetList {0: CSSStyleSheet, length: 1}
    textContent: "img { width: 200px; }"
  ► __proto__: ShadowRoot
```
#### mode: 'closed'
Значение  **_`'closed'`_**  делает shadow DOM  данного элемента недоступным для скриптов

При обращении к свойству shadowRoot  элемента  будет возвращено значение  `null`

###### Доступные свойства shadowRoot
```javascript
console.dir ( elem.shadowRoot )
```
```console
null
```
***
[### 💼 Упражнения](https://docs.google.com/forms/d/e/1FAIpQLSdjCWOSAVFqZqcm4sy-q-KBFmd1i2BbfYQ0pcZaqYb9YZyv5w/viewform)