# :mortar_board: Генераторы и итераторы
###### ES6

### Генератор

Функция-генератор объявляется с помощью ключевого слова **`function*`**<br/>
:warning: **`*`** - обязательный атрибут функции-генератора

С помощью функции-генератора создается объект-итератор<br/>
Функция-генератор  определяет порядок итерирования данных,<br/>
который зависит от структуры данных

Сама по себе функция-генератор ничего не итерирует и ничего не возвращает,<br/>
кроме, как уже было сказано, объекта-итератора

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
С помощью этого метода итератор переходит от текущего элемента структуры данных к следующему
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