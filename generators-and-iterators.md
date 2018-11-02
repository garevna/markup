# :mortar_board: Генераторы и итераторы
###### ES6

### Генератор

Функция-генератор объявляется с помощью ключевого слова **`function*`**<br/>
:warning: **`*`** - обязательный атрибут функции-генератора

С помощью функции-генератора создается объект-итератор<br/>
Функция-генератор  определяет порядок итерирования данных,<br/>
который зависит от структуры данных

Сама по себе функция-генератор ничего не итерирует и ничего не возвращает,<br/>
кроме, как уже было сказано, объекта-**итератора**

Именно поэтому генератор <br/>
вместо оператора  **`return`**<br/>
использует оператор  **`yield`**<br/>
```javascript
function* generator ( ... ) {
    ...
    yield ...
}
```
Оператор  **`yield`** позволяет управлять работой итератора<br/>
Этим оператором функция-генератор говорит итератору, <br/>
что в этом месте нужно остановиться и вернуть текущее значение
```javascript
function* colorsGenerator () {
    while ( true ) {
        yield `rgb(
            ${Math.round ( Math.random() * 255 )},
            ${Math.round ( Math.random() * 255 )},
            ${Math.round ( Math.random() * 255 )}
        )`
    }
}

let colorIterator = colorsGenerator ()

for ( var x=0; x < 100; x++ ) {
    let point = document.body.appendChild (
        document.createElement ( 'div' )
    )
    point.style = `
        float: left;
        width: 10px;
        height: 10px;
        background-color: ${ colorIterator.next().value};
    `
}
```
У объекта-итератора есть обязательный метод **`next()`**<br/>
С помощью этого метода итератор переходит от текущего элемента структуры данных к следующему<br/>
Этот метод возвращает объект с двумя свойствами:    **`value`**  и  **`done`**

✅ Свойство  **`value`**  содержит текущий элемент структуры данных

✅ Свойство  **`done`**  принимает значение  `true`, когда процесс итерирования структуры данных завершен

Собственно говоря, алгоритм работы итератора описывается в генераторе

Вот так "рождается" итератор со встроенным алгоритмом итерирования массива данных
```javascript
var iterator = generator ( ... )
```
```javascript
var user = {
    login: "Сергей",
    avatar: "https://www.shareicon.net/data/2015/12/14/207817_face_300x300.png",
    email: "serg789@gmail.com",
    place ( tagName ) {
        return document.body.appendChild (
            document.createElement ( tagName )
        )
    },
    showAvatar () {
        let ava = this.place ( "img" )
        ava.src = this.avatar
        ava.width = "70"
        return ava
    },
    showLogin () {
        let x = this.place ( "h3" )
            .innerHTML = this.login
        return x
    },
    showEmail () {
        let x = this.place ( "p" )
            .innerHTML = this.email
        return x
    }
}

user.generator = function* () {
    yield this.showLogin ()
    yield this.showEmail ()
    yield this.showAvatar ()
}

user.iterator = user.generator ()
while ( !user.iterator.next().done ) {}
// user.iterator.next()  // {value: "Сергей", done: false}
// user.iterator.next()  // {value: "serg789@gmail.com", done: false}
// user.iterator.next()  // {value: img, done: false}
// user.iterator.next()  // {value: undefined, done: true}
```
#### Symbol.iterator
Если у объекта есть свойство  **`Symbol.iterator`**, то этот объект является итерабельным<br/>
( то есть можно перебирать его свойства оператором for...of )

**`Symbol.iterator`**  является ссылкой на функцию-генератор

:coffee: :one:
```javascript
var user = {
    login: "Сергей",
    avatar: "https://www.shareicon.net/data/2015/12/14/207817_face_300x300.png",
    email: "serg789@gmail.com",
    hobby: [ "football", "fishing" ],
    place: document.body.appendChild (
        document.createElement ( "figure" )
    ),
    showAvatar () {
        let ava = this.place.appendChild (
            document.createElement ( "img" )
        )
        ava.src = this.avatar
        ava.width = "70"
    },
    showLogin () {
        this.place.appendChild (
            document.createElement ( "h3" )
        ).innerHTML = this.login
    },
    showEmail () {
        this.place.appendChild (
            document.createElement ( "p" )
        ).innerHTML = this.email
    }
}

user [ Symbol.iterator ] = function* () {
        yield this.showLogin ()
        yield this.showEmail ()
        yield this.showAvatar ()
}
```
✍ Добавим свойство  **_iterator_**  объекту  **user**:
```javascript
user.iterator = user [ Symbol.iterator ]()
```
✊ Теперь в свойстве  **_iterator_**  объекта  **user** находится ссылка на итератор

Вызовем его:
```javascript
user.iterator.next()
```
Чтобы заставить итератор отработать до конца:
```javascript
while ( !user.iterator.next().done ) {}
```

:coffee: :two:
###### Строка текста
```javascript
function* someGenerator ( startValue, endValue ) {
    var y = startValue
    while ( y < endValue ) 
        yield y += String.fromCharCode ( y.charCodeAt( y.length-1 ) + 1 )
}
var someIterator = someGenerator ( "a", "abcdef" )
```

:coffee: :three:
###### Связные списки
```javascript
function* someGenerator ( objs ) {
    var currentItem = objs [ 0 ]
    var nextItem = objs [ 0 ]
    while ( !!nextItem ) {
        currentItem = nextItem
        nextItem = !!currentItem.nextItem ? 
            objs.find ( x => currentItem.nextItem === x.val )
            : null
        yield currentItem.val
    }
}

var objects = [
    { val: "first",       nextItem: "second" },
    { val: "forth",      nextItem: "fifth" },
    { val: "sixth",      nextItem: null },
    { val: "third",      nextItem: "forth" },
    { val: "fifth",       nextItem: "sixth" },
    { val: "second", nextItem: "third" }
]

var iterator = someGenerator ( objects )
```

:coffee: :four:
```javascript
function* elemsGenerator ( elemsProps ) {
    for ( let elemData of elemsProps ) {
        yield ( elem => {
            var el = document.createElement ( elem.tagName )
            document.body.appendChild ( el )
            if ( elem.attrs ) 
                for ( var x in elem.attrs ) {
                    el [ x ] = elem.attrs [ x ]
                }
            return el
        })( elemData )
    }
}

var elems = [
    { tagName: "div", attrs: { id: "first", className: "first" } },
    { tagName: "article", attrs: { id: "second", className: "second" } },
    { tagName: "figure", attrs: { id: "third", className: "third" } },
    { tagName: "p", attrs: { id: "forth", className: "forth" } }
]

var newElement = elemsGenerator ( elems )
```
***
### [:briefcase: Упражнения](https://docs.google.com/forms/d/e/1FAIpQLSf3HcSENvJodCQjaW_azeh_lMXwCD6HsRq3adiPnyqRFm_6Vg/viewform)