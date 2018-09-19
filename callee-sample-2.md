[:arrow_backward:](function-object#callee) **arguments.callee**

#### :coffee: 2

Объявим функцию  **`getArguments`**:
```javascript
function getArguments ( param ) {
    return param ? param : arguments.callee
}
```
которая, если ей был передан аргумент, возвращает значение этого аргумента, в противном случае возвращает ссылку на саму себя

Теперь вызовем эту функцию с параметром и без:

```javascript
var x = getArguments ()
var y = getArguments ( "Привет!" )
```
результат вызова функции без аргументов мы поместили в переменную  **`x`**,

а результат вызова с аргументом "Привет!" мы поместили в переменную  **`y`**

Теперь выведем в консоль переменные **`x`** и **`y`**

в переменной **`x`** находится точная копия функции **`getArguments`**

а в переменной **`y`** - строка "Привет!"

Вызовем функцию **`x`**:
```javascript
x ( "До свидания!" )
```
и получим строку "До свидания!"

[:arrow_backward:](function-object#callee) **arguments.callee**