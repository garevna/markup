## :mortar_board: valueOf

Метод  **valueOf ()**  есть у каждого объекта

Этот метод вызывается автоматически, когда необходимо вернуть примитивное значение объекта

Например, если объект сравнивается с числом
```javascript
var obj = {
   num: 5,
   val: 10,
   x: 11,
   valueOf: function () {
      return this.num + this.val - this.x
   }
}
```
Если теперь мы выполним сравнение:
```javascript
obj == 4
```
то получим  *`true`*

При выполнении сравнения будет вычисляться примитивное значение объекта, т.е. вызываться метод **`valueOf`**

Если примитивное значение объекта вычислить невозможно, то будет возвращен сам объект

**`valueOf ()`** - **__унаследованный__** метод любого объекта

Но это не означает, что мы не можем его переопределить

:coffee: 1

```javascript
var human = {
   name: "Ivan",
   age: 25,
   valueOf: function () {
      return this.name + ": " + this.age
   }
}

console.info ( human + "!" ) // Ivan: 25!
```
:coffee: 2

Конечно, так делать не стоит, но все-таки интересно :wink:

в результате выполнения следующего кода:
```javascript
Object.prototype.valueOf = function () {
    return "Это объект, блин, а не игрушка!"
}
```
все нативные объекты JS будут "ругаться" соответствующим образом при попытке получить их примитивное значение
```javascript
console.info ( Number + "" )
```
```console
Это объект, блин, а не игрушка!
```
:coffee: 3

```javascript
const test = {
   num: 0,
   valueOf: function () {
      return this.num += 1
   }
}
```
:grey_question: Что вернет выражение: 
```javascript
test == 1 && test == 2 && test == 3
```
***
### [:briefcase: Упражнения](https://docs.google.com/forms/d/e/1FAIpQLSf9YlXTMs5oCuSWEtPdhZiOeiLTPWejH4zRY7jHoJbrnJEwrA/viewform)