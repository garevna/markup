<a name="top"></a>
# :mortar_board: Элементы DOM 

| [:arrow_double_down:](#bottom) | <img width="800"/> | [:arrow_heading_down:](#appendChild) |
|-|-|-|

## Методы

| | |
|-|-|
|[:arrow_right_hook:](#appendChild) `appendChild`|[:arrow_right_hook:](#removeChild)`removeChild`|
|[:arrow_right_hook:](#insertBefore) `insertBefore`|[:arrow_right_hook:](#replaceChild) `replaceChild`|
|[:arrow_right_hook:](#insertAdjacentHTML) `insertAdjacentHTML`|[:arrow_right_hook:](#insertAdjacentElement) `insertAdjacentElement`|
|[:arrow_right_hook:](#setAttribute) `setAttribute`|[:arrow_right_hook:](#getAttribute) `getAttribute`|
|[:arrow_right_hook:](#getBoundingClientRect) `getBoundingClientRect`|[:arrow_right_hook:](#scrollIntoView) `scrollIntoView`|
|[:arrow_right_hook:](#addEventListener) `addEventListener`|[:arrow_right_hook:](#removeEventListener) `removeEventListener`|

<a name="appendChild"></a>
##### ✅ appendChild()

| [:arrow_heading_up:](#top) | <img width="800"/> | [:arrow_heading_down:](#removeChild) |
|-|-|-|

Добавляет элементу дочерний элемент

### :coffee: :one:
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

### :coffee: :two:

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

### :coffee: :three:

```javascript
var script = document.createElement ( 'script' )
script.appendChild (
    document.createTextNode (
        `alert ( "Hello" )`
    )
)
document.body.appendChild ( script )
```
<a name="removeChild"></a>
##### ✅ removeChild()

| [:arrow_heading_up:](#appendChild) | <img width="800"/> | [:arrow_heading_down:](#insertBefore) |
|-|-|-|

Удаление элемента

:warning: `Удалить элемент может только его непосредственный родитель`

### :coffee: :four:
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
<a name="insertBefore"></a>
##### ✅ insertBefore()

| [:arrow_heading_up:](#removeChild) | <img width="800"/> | [:arrow_heading_down:](#insertAdjacentHTML) |
|-|-|-|

### :coffee: :five:
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
<a name="insertAdjacentHTML"></a>
##### ✅ insertAdjacentHTML()

| [:arrow_heading_up:](#insertBefore) | <img width="800"/> | [:arrow_heading_down:](#insertAdjacentElement) |
|-|-|-|

### :coffee: :six:

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
<a name="insertAdjacentElement"></a>
##### ✅ insertAdjacentElement()

| [:arrow_heading_up:](#insertAdjacentHTML) | <img width="800"/> | [:arrow_heading_down:](#props) |
|-|-|-|

### :coffee: :seven:

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
***
<a name="props"></a>
### Свойства 

##### ✅ **`childNodes`**

`Объект` [**`NodeList`**](nodeTypes "Типы узлов дерева DOM")

| [:coffee: :eight:](childNodes-sample-1) |
|-|

[🔗 w3schools](https://www.w3schools.com/jsref/prop_node_childnodes.asp)
***
##### ✅ **`children`**

`Объект` **`HTMLCollection`**

##### ✅ **`parentNode`**

`Ссылка на родительский элемент ( контейнер, в котором находится элемент )`

### :coffee: :nine:
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

##### ✅ **`on`** + тип события

Все свойства элементов DOM, начинающиеся на **`on`**, являются потенциальными ссылками на обработчика соответствующего события

Изначально они имеют значение **null**

### :coffee: :keycap_ten:

```javascript
var section = document.body.appendChild (
     document.createElement ( 'section' )
)
section.innerHTML = "<h3>Hello</h3>"

for ( var prop in section ) {
     if ( prop.indexOf ( 'on' ) !== 0 ) continue
     console.info ( `Event: ${prop.slice(2)}` )
}
```
***
### [:briefcase: Упражнения](https://docs.google.com/forms/d/e/1FAIpQLSfOAAnZrszP3EiO3zgYzfkqBpH68ggE9mFzsDyK40_WUjB89A/viewform)