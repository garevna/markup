# :mortar_board: Элементы DOM 

### Свойства 

##### ✅ **`childNodes`**

`Объект` [**`NodeList`**](nodeTypes "Типы узлов дерева DOM")

| [:coffee: 1](childNodes-sample-1) |
|-|

[🔗 w3schools](https://www.w3schools.com/jsref/prop_node_childnodes.asp)
***
##### ✅ **`children`**

`Объект` **`HTMLCollection`**

##### ✅ **`parentNode`**

`Ссылка на родительский элемент ( контейнер, в котором находится элемент )`

### :coffee: :two:
```html
<body>
    <div id="demo">
        <section id="section"></section>
        <figure></figure>
    </div>
</body>
```
```javascript
var section = document.querySelector ( "#section" )
console.dir ( section.parentNode )  // ► div#demo
```

## Методы

##### ✅ appendChild()

Добавляет элементу дочерний элемент

### :coffee: :three:
```html
<body>
    <div id="demo">
        <section></section>
        <figure></figure>
    </div>
</body>
```
```javascript
var section = document.createElement ( "section" )
section.innerHTML = "Hello"
document.querySelector ( "#demo" ).appendChild ( section )
```
Результат:
```html
<body>
    <div id="demo">
        <section>Hello</section>
    </div>
</body>
```

### :coffee: :four:

```javascript
var style = document.createElement ( 'style' )
document.head.appendChild ( style )
style.innerText = `p { color: red; }`

style.sheet.cssRules[0]          // объект
style.sheet.cssRules[0].cssText  // "p { color: red; }"

style.appendChild (
    document.createTextNode (
        `div { color: blue; }`
    ) 
)
```
Результат:
```html
<head>
    <style>
        p { color: red; }
        div { color: blue; }
    </style>
</head>
```

### :coffee: :five:

```javascript
var script = document.createElement ( 'script' )
script.appendChild (
    document.createTextNode (
        `alert ( "Hello" )`
    )
)
document.body.appendChild ( script )
```

##### ✅ removeChild()

Удаление элемента

:warning: `Удалить элемент может только его непосредственный родитель`

### :coffee: :six:
```html
<body>
    <div id="demo">
        <section id="section"></section>
        <figure class="figure"></figure>
    </div>
</body>
```
```javascript
var section = document.querySelector ( "#section" )
var removed = section.parentNode.removeChild ( section )
console.dir ( removed )  // ► section#section

var figure = document.querySelector ( ".figure" )
figure.appendChild ( removed )
```
```html
<body>
    <div id="demo">
        <figure class="figure">
            <section id="section"></section>
        </figure>
    </div>
</body>
```

##### ✅ insertBefore()

### :coffee: :seven:
```javascript
function addElement ( tagName, container ) {
    var _container = 
        container && container.nodeType === 1 ? 
           container : document.body
    return _container.appendChild (
         document.createElement ( tagName )
    )
}

var main = addElement ( "main" )
var section = addElement ( "section", main )
var figure = addElement ( "figure", main )

main.insertBefore ( document.createElement ( "p" ), section )
```
##### ✅ insertAdjacentHTML()

### :coffee: :eight:

Используя функцию addElement из предыдущего примера, вставим на страницу элементы _`main`_, _`section`_ и _`figure`_:

```html
<body>
    <main>
        <section></section>
        <figure></figure>
    </main>
</body>
```
А теперь выполним следующий код в консоли:
```javascript
section.insertAdjacentHTML ( `beforeBegin`, `<p>Hello</p>` )
section.insertAdjacentHTML ( `afterBegin`, `<p>Let's work</p>` )
section.insertAdjacentHTML ( `beforeEnd`, `<p>I've finished</p>` )
section.insertAdjacentHTML ( `afterEnd`, `<p>Bye</p>` )
```
Результат во вкладке Elements:
```html
<body>
    <main>
        <p>Hello</p>
        <section>
            <p>Let's work</p>
            <p>I've finished</p>
        </section>
        <p>Bye</p>
        <figure></figure>
    </main>
</body>
```

##### ✅ insertAdjacentElement()

### :coffee: :nine:

```html
<body>
    <main>
        <section id="demo">
        </section>
        <figure></figure>
    </main>
</body>
```
```javascript
document.getElementById ( "demo" )
    .insertAdjacentElement( 
        "beforeend",
        document.createElement ( "p" )
    )
document.querySelector ( "figure" )
    .insertAdjacentElement( 
        "afterend",
        document.createElement ( "h3" )
    )
document.querySelector ( "#demo" )
    .insertAdjacentElement( 
        "beforebegin",
        document.createElement ( "img" )
    )
document.getElementsByTagName ( "figure" )[0]
    .insertAdjacentElement( 
        "afterbegin",
        document.createElement ( "li" )
    )
```
Результат во вкладке Elements:
```html
<body>
    <main>
        <img>
        <section id="demo">
            <p></p>
        </section>
        <figure>
            <li></li>
        </figure>
        <h3></h3>
    </main>
</body>
```