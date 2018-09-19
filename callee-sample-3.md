[:arrow_backward:](function-object#callee) **arguments.callee**

#### :coffee: 3

Объявим функцию, которая "сама себя лечит", т.е. сама добавляет себе свойства и методы:

```javascript
function setProperty ( prop, val ) {
    arguments.callee [ prop ] = val
}
```
Теперь заставим ее создать себе парочку свойств:
```javascript
setProperty ( "isActive", false )
setProperty ( "value", 50 )
```
Ну, и для пущей убедительности заставим ее создать себе метод:
```javascript
setProperty ( "method", function () {
    console.log ( "А еще я умею вышивать крестиком" )
} ) 
```
здесь мы передаем ей в качестве второго аргумента функцию

Теперь проверим, что эти свойства и метод появились у функции  **`setProperty`**

Выведем в консоль свойства **`isActive`** и **`value`**   функции  **`setProperty`**  и вызовем ее метод  **`method`**

[:arrow_backward:](function-object#callee) **arguments.callee**