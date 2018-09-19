[:arrow_backward:](function-object#callee) **arguments.callee**

#### :coffee: 4

Создадим функцию, которая "накапливает" результаты собственных вычислений

Пусть это будет функция, вычисляющая факториал числа

```javascript
var factorial = function ( num ) {
        var res = 1, n = 1
        while ( n <= num )  res *= n++
}
```

"модифицируем" ее следующим образом:

```javascript
var factorial = function ( num ) {
     if ( !arguments.callee.res )  arguments.callee.res = []
     var res = 1, n = 1
     while ( n <= num )  res *= n++
     arguments.callee.res.push ( res )
     return res
}
```
Вызовем ее с различными значениями аргумента и выведем в консоль значение свойства **`res`**:
```javascript
factorial ( 5 )
factorial ( 5 )

console.log ( factorial.res )
```
Получим массив *[ 120, 3628800 ]*

[:arrow_backward:](function-object#callee) **arguments.callee**