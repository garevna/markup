<a name="top"></a>
# :mortar_board: Статические методы конструктора  Object

| ES5 |
|-|
| ✅ Object.assign() | 
| ✅ Object.create()
| ✅ Object.defineProperty() |
| ✅ Object.defineProperties() |
| Object.freeze() |
| ✅ Object.getOwnPropertyDescriptor() |
| [**`Object.getOwnPropertyNames()`**](#objectgetownpropertynames-) |
| Object.getOwnPropertySymbols() |
| Object.getPrototypeOf() |
| Object.is() |
| Object.isExtensible() |
| Object.isFrozen() |
| Object.isSealed() |
| [**`Object.keys()`**](#objectkeys) |
| Object.preventExtensions() |
| Object.seal() |
| Object.setPrototypeOf() |
| **ES8 ( 2017 )** |
| [**`Object.values()`**](#mortar_board-objectvalues) |
| [**`Object.entries()`**](#mortar_board-objectentries) |
| [**`Object.getOwnPropertyDescriptors()`**](#mortar_board-objectgetownpropertydescriptors) |
***
[:link: MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)

## :mortar_board: Object.keys()
> ###### возвращает массив всех **_собственных перечислимых_** свойств экземпляра
> ###### аргумент - ссылка на экземпляр
:coffee:
```javascript
var Human = function () {
    this.name = arguments [ 0 ] || "Тимофей"
    this.age = arguments [ 1 ] || 25
    this.speciality = arguments [ 2 ] || "слесарь"
}

Human.prototype.setSpeciality = function ( spec ) {
    this.speciality = spec
}

var man = new Human ( null )
```
:coffee: <code>Добавим в прототип **Human** новое свойство **_employed_**:</code>
```javascript
Human.prototype.employed = false
console.log ( man.employed )  // false
```    
:coffee: <code>выведем в консоль собственные перечислимые свойства экземпляра  **man**</code>
```javascript
console.log ( Object.keys ( man ) )
```
###### Результат:
```console
(3) [ "name", "age", "speciality" ]
```
:coffee: <code>выведем перечислимые свойства прототипа:</code>
```javascript
console.log ( Object.keys ( Human.prototype ) )
```
###### Результат:
```console
(2) [ "setSpeciality", "employed" ]
```
:coffee: <code>Выполним присваивание:</code>
```javascript
man.employed = true
console.log ( Object.keys ( man ) )
```
###### Результат:
```console
(4) [ "name", "age", "speciality", "employed" ]
```
> <code>у экземпляра **man** появилось собственное свойство  **_employed_**, но у прототипа и экземпляра это совершенно различные свойства:</code>
```javascript
console.log ( man.employed )           // true
console.log ( man.__proto__.employed ) // false
```

| [:arrow_double_up:](#top) |
|-|

## :mortar_board: Object.getOwnPropertyNames()
```javascript
```

| [:arrow_double_up:](#top) |
|-|

## :mortar_board: Object.getOwnPropertyDescriptor()
```javascript
```

| [:arrow_double_up:](#top) |
|-|

## :mortar_board: Object.defineProperty()
```javascript
```

| [:arrow_double_up:](#top) |
|-|

## :mortar_board: Object.defineProperties()
```javascript
```

| [:arrow_double_up:](#top) |
|-|

## :mortar_board: Object.assign()
```javascript
```

| [:arrow_double_up:](#top) |
|-|

## :mortar_board: Object.getOwnPropertyDescriptors()
###### ES8 ( 2017 )
Получает объект<br/>
Возвращает объект<br/>
Имена свойств возвращаемого объекта - это имена свойств объекта-аргумента<br/>
Значения свойств возвращаемого объекта - это дескрипторы свойств объекта-аргумента<br/>
```javascript
var obj = {
        name: "first",
        type: "circle",
        color: "red",
        radius: 100,
        center: [ 120, 120 ]
}

Object.getOwnPropertyDescriptors( obj )
```
###### Результат:
```console
▼ {name: {…}, type: {…}, color: {…}, radius: {…}, center: {…}}
  ► center: {value: Array(2), writable: true, enumerable: true, configurable: true}
  ► color: {value: "red", writable: true, enumerable: true, configurable: true}
  ► name: {value: "first", writable: true, enumerable: true, configurable: true}
  ► radius: {value: 100, writable: true, enumerable: true, configurable: true}
  ► type: {value: "circle", writable: true, enumerable: true, configurable: true}
  ► __proto__: Object
```

| [:arrow_double_up:](#top) |
|-|

## :mortar_board: Object.values()
###### ES8 ( 2017 )
Возвращает **массив** **_значений_** собственных перечислимых свойств экземпляра,
т.е. тех свойств, имена которых возвращает метод **`Object.keys()`**
```javascript
var obj = {
    name: "first",
    type: "circle",
    color: "red",
    radius: 100,
    center: [ 120, 120 ]
}

console.log ( Object.values( obj ) )
```
###### Результат:
```console
(5) ["first", "circle", "red", 100, Array(2)]
```

| [:arrow_double_up:](#top) |
|-|

## :mortar_board: Object.entries()
###### ES8 ( 2017 )
Возвращает массив собственных перечислимых свойств экземпляра<br/>
в виде массива из двух элементов: имени свойства и его значения  
```javascript
var obj = {
    name: "first",
    type: "circle",
    color: "red",
    radius: 100,
    center: [ 120, 120 ]
}

console.log ( Object.entries( obj ) )
```
###### Результат:
```console
▼ (5) [Array(2), Array(2), Array(2), Array(2), Array(2)]
  ► 0: (2) ["name", "first"]
  ► 1: (2) ["type", "circle"]
  ► 2: (2) ["color", "red"]
  ► 3: (2) ["radius", 100]
  ► 4: (2) ["center", Array(2)]
    length: 5
  ► __proto__: Array(0)
```
###### :coffee: :one: Нарисуем окружность
```javascript
var obj = {
    width: "30%",
    height: "30%",
    border: "solid 1px red",
    borderRadius: "50%",
    position: "fixed",
    top: "10%",
    left: "10%"
}
var elem = document.body.appendChild (
    document.createElement ( "div" )
)
Object.entries( obj )
   .forEach ( prop => elem.style [ prop [0] ] = prop [1] )
```

###### :coffee: :two: Выведем все свойства объекта **obj** в консоль
```javascript
console.info ( 'obj = {\n' )
for ( var x of Object.entries( obj ) ) {
    console.info ( `     ${x[0]}:${x[1]}\n` )
}
console.info ( '}' )
```
###### Результат:
```console
obj = {
      width:30%
      height:30%
      border:solid 1px red
      borderRadius:50%
      position:fixed
      top:10%
      left:10%
}
```

| [:arrow_double_up:](#top) |
|-|



| [:arrow_double_up:](#top) |
|-|



| [:arrow_double_up:](#top) |
|-|



| [:arrow_double_up:](#top) |
|-|



| [:arrow_double_up:](#top) |
|-|



| [:arrow_double_up:](#top) |
|-|