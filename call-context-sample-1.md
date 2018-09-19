[:arrow_backward:](function-object#call-context) **Контекст вызова**

#### :coffee: 1

Объявим три функции:

```javascript
function first () {
        console.log ( "Работает функция first" )
}
function second () {
        console.log ( "Работает функция second" )
}
function third () {
        console.log ( "Работает функция third" )
}
```
Все три функции объявлены в глобальном контексте, то есть они являются методами глобального объекта **`window`**

Как мы уже знаем, можно обращаться к свойствам объекта как к элементам ассициативного массива

Тогда конструкция:
```javascript
window [ "first" ]
```
вернет нам функцию  **`first`**, которая является свойством ( методом ) глобального объекта **`window`**

Для вызова этой функции не хватает только круглых скобок:
```javascript
window [ "first" ] ()
```
Используя этот факт, мы можем вызывать функцию, имя которой нам передано в переменной типа "*string*":
```javascript
for ( var func of [ "first", "second", "third" ] ) 
    window [ func ] ()
```

[:arrow_backward:](function-object#call-context) **Контекст вызова**