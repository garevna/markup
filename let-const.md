# :mortar_board: let | const
###### ES6 ( 2015 )
***
### let
###### Блочная область видимости:
```javascript
var x = 5
{
    let x = 15
    console.log ( x )
}
console.log ( x )
```
###### Невозможно повторно объявить переменную с таким же идентификатором в той же области видимости:
```javascript
function sample () {
    let figure = {
        name: "Radius",
        size: 50
    }
    console.log ( figure )
    let figure = 10
    console.log ( figure )
}
sample ()
```
###### Будет сгенерировано исключение: 
```console
⛔️ Uncaught SyntaxError: Identifier 'figure' has already been declared
```
###### Однако в цикле сработает, потому что явно присутствует блок {...}
```javascript
let sample = { a: 'img', b: 'div', c: 'p' }
for ( let prop in sample ) {
    let elem = document.body.appendChild ( 
        document.createElement ( sample [ prop ] )
    )
    console.log ( elem )
}
```
###### `let` не создает свойств в глобальном объекте
```javascript
var x = 25
let z = 15
window.x    //  25
window.z    //  undefined
```
###### `let` создает "замыкание" без замыкания:
```javascript
for ( let i of [ 1, 2, 3, 4, 5 ] ) {
    setTimeout ( () => console.log ( i ), 1000 * i )
}
```
###### :warning: hoisting не работает с `let` ( объявления с  `let` не поднимаются )
***
### const
###### Блочная область видимости ( как у `let` )
###### Невозможно дублирование объявления ( как у `let` )
###### В общем, все, как у `let`, только:
###### :warning: Изменить значение нельзя
```javascript
const XXX = 11
XXX = 55
```
Будет сгенерировано исключение: 
```console
⛔️ Uncaught TypeError: Assignment to constant variable.
```
###### Обязательно при объявлении инициализировать значение
```javascript
const XXX
```
Будет сгенерировано исключение: 
```console
⛔️ Uncaught SyntaxError: Missing initializer in const declaration
```
###### Если константа является объектом, то значения ее свойств могут быть изменены:
```javascript
const USER = {
    login: "admin",
    role: "admin",
    status: "active",
    rights: [ "read", "write", "delete" ]
}

USER.login = "student"
USER.role = "user"
USER.rights = [ "read" ]
```
###### Аналогично с массивами:
```javascript
const RIGHTS = [ "read", "write", "delete" ]
RIGHTS [ 1 ] = null
RIGHTS [ 2 ] = null
```
***
### [:briefcase: Упражнения](https://docs.google.com/forms/d/e/1FAIpQLScPBbEkpMk9CNH935pToTh_BmyE1vqk2rnzu3Mhw9F-D-7V_w/viewform)