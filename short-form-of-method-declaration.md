## :mortar_board: Краткая форма объявления методов
###### ES6
✋ Краткий синтаксис объявления методов при инициализации объекта:
```javascript
var user = {
    name: "Ivan",
    sayHello () {
        console.log ( `Hello, ${ this.name }!` )
    },
    sayBye () {
        console.log ( `Bye, ${ this.name }!` )
    }
}
user.sayHello ()
user.sayBye ()
```
:warning: Вместо 
```javascript
sayHello: function () {
    console.log ( `Hello, ${ this.name }!` )
}
```
можно использовать краткую форму: 
```javascript
sayHello () {
    console.log ( `Hello, ${ this.name }!` )
}
```
:warning: Краткий синтаксис допускает вычисляемые имена свойств
```javascript
var bag = {
    [ "thing" + 0 ]: "👜",
    thing1: function () { return '🌹' },
    thing2 () { return "🌸" },
    [ "thing" + 3 ] () { return "🍄" },
}
console.log ( bag.thing0 )
console.log ( bag.thing1 () )
console.log ( bag.thing2 () )
console.log ( bag.thing3 () )
```