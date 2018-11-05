# :mortar_board: &lt;template>

    ✅ DocumentFragment
    ✅ content
    ✅ cloneNode ()

Элемент &lt;template> предназначен для хранения шаблона разметки
###### :warning: Он не отображается на странице
###### :warning: Он парсится браузером, поэтому должен содержать только валидный код разметки

:coffee: :one:
###### Откроем вкладку _Elements_ инструментов разработчика и вставим в элемент `body` следующий код разметки:
```html
<body>
    <template id="sample">
        <h3>Template header</h3>
        <p>Template text</p>
    </template>
</body>
```
При этом на странице ничего не появится, а вот во вкладке  **Elements**  мы увидим следующую картинку
```html
▼ <template id="sample">
  ▼ #document-fragment
     <h3>Template header</h3>
     <p>Template text</p>
  </template>
```
## :mortar_board: DocumentFragment
это фрагмент документа, у которого нет родителя в дереве DOM

DocumentFragment содержит DOM-элементы ( nodes ), как и объект document

Но поскольку фрагмент документа не является частью структуры DOM, он не отображается на странице

Это шаблон разметки, который при необходимости может быть вставлен в нужное время в нужном месте

### :mortar_board: content
###### Свойство  _content_  элемента  `template`  содержит код разметки, находящийся  в контейнере <code>&lt;template>...&lt;/template></code>


:coffee: :two:
###### Шаблон разметки
```html
<template id="svg">
    <svg width="400" height="400">
        <circle cx="200" cy="200" 
                r="100" 
                fill="transparent"
                stroke="red" 
                style="stroke-width:5">
        </circle>
    </svg>
</template>
```
###### Выведем в консоль свойство `content`
```javascript
const circle = document.querySelector ( "#svg" )
console.dir ( circle.content )
```
###### Результат
```console
▼ #document-fragment
    baseURI: "about:blank"
    childElementCount: 2
  ► childNodes: NodeList(5) [text, h3, text, p, text]
  ► children: HTMLCollection(2) [h3, p]
  ► firstChild: text
  ► firstElementChild: h3
    isConnected: false
  ► lastChild: text
  ► lastElementChild: p
    nextSibling: null
    nodeName: "#document-fragment"
    nodeType: 11
    nodeValue: null
  ► ownerDocument: document
    parentElement: null
    parentNode: null
    previousSibling: null
    textContent: "↵        Template header↵        Template text↵    "
  ► __proto__: DocumentFragment
```
### Вставка в DOM

Если выполнить код:
```javascript
document.body.appendChild ( circle.content )
```
то после вставки в DOM содержимого шаблона контейнер  `<template id="svg"></template>`  будет пустым

Можно проверить это:
```javascript
console.dir ( circle.content )
```
Свойство  **`childNodes`**  будет  **_`NodeList [ ]`_**       ( пустая коллекция узлов )

Свойство  **`children`**  будет  **_`HTMLCollection [ ]`_**   ( пустая коллекция элементов )

:warning: Для многоразового использования шаблона разметки нужно использовать метод **cloneNode ( `true` )**
```javascript
document.body.appendChild ( circle.content.cloneNode ( true ) )
```
###### ✋ true указывает на глубокое копирование, т.е. всех подузлов дерева

:coffee: :one:
###### Шаблон разметки
```html
<template id="sample">
    <style>
        svg { border: dotted 1px; }
        circle { stroke-width:5; }
    </style>
    <svg width="400" height="400" id="svg">
        <circle cx="200" cy="200" r="100" 
                id="circle"
                fill="transparent" 
                stroke="red">
        </circle>
    </svg>
</template>
```
###### Класс
```javascript
class CanvasElement extends HTMLElement {
    constructor () {
        super()
        var shadow = this.attachShadow ( { mode: 'open' } )
        var sample = document.querySelector ( "#sample" )
        shadow.appendChild ( sample.content )
    }
}
customElements.define ( 'canvas-element', CanvasElement )
```
###### Вставка на страницу
```html
<canvas-element></canvas-element>
```