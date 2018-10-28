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
| ES8 ( 2017 ) |
| ✅ Object.values () |
| ✅ Object.entries () |
| ✅ Object.getOwnPropertyDescriptors () |
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
```javascript
```

| [:arrow_double_up:](#top) |
|-|

## :mortar_board: Object.values()
###### ES8 ( 2017 )
```javascript
```

| [:arrow_double_up:](#top) |
|-|

## :mortar_board: Object.entries()
###### ES8 ( 2017 )
```javascript
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