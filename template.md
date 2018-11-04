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
Свойство  **_content_**  элемента  `template`  содержит код разметки, находящийся  в контейнере  
<code>
&lt;template>...&lt;/template>
</code>

var circle = document.querySelector ( "#svg" )
console.dir ( circle.content )

:coffee: :two:
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

```javascript
const circle = document.querySelector ( "#svg" )
console.dir ( circle.content )
```
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