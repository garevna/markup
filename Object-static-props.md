<a name="top"></a>
# :mortar_board: Статические методы конструктора  Object

| ES5 | |
|-|-|
| ✅ Object.assign() |  [**`Object.defineProperty()`**](#mortar_board-objectdefineproperty) |
| ✅ Object.create() | ✅ Object.defineProperties() |
| Object.freeze() | [**`Object.getOwnPropertyDescriptor()`**](#mortar_board-objectgetownpropertydescriptor) |
| Object.is() | [**`Object.getOwnPropertyNames()`**](#objectgetownpropertynames-) |
| Object.isExtensible() | Object.getOwnPropertySymbols() |
| Object.isFrozen() | Object.getPrototypeOf() |
| Object.isSealed() | [**`Object.keys()`**](#objectkeys) |
| Object.seal() | Object.preventExtensions() |
| Object.setPrototypeOf() | [**`Object.getOwnPropertyDescriptors()`**](#mortar_board-objectgetownpropertydescriptors) |
| [**`Object.values()`**](#mortar_board-objectvalues) | [**`Object.entries()`**](#mortar_board-objectentries) | |

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
Возвращает имена собственных свойств объекта

Свойства объекта могут быть функциями ( методы )
```javascript
var funcObject = {
    getName() {},
    setName() {}
}
var newObject = Object.assign (
    {},
    { name: "Егор", age: 25 },
    {  write: true, read: true  },
    funcObject
)
Object.getOwnPropertyNames ( newObject )
```
###### Результат:
```console
(6) ["name", "age", "write", "read", "getName", "setName"]
```

| [:arrow_double_up:](#top) |
|-|

## :mortar_board: Object.getOwnPropertyDescriptor()

###### Этот метод позволяет получить дескриптор собственного свойства объекта
###### Возвращает объект дескриптора свойства
###### Первым аргументом метода является объект
###### второй аргумент - имя свойства объекта

### Атрибуты свойств
<code>Для каждого свойства объекта существует **дескриптор свойства**</code><br/>
<code>Дескриптор свойства - это объект</code><br/>
<code>Он содержит атрибуты свойства:</code>
###### ✋ value
> <code>значение свойства</code><br/>
> <code>( по умолчанию _undefined_ )</code>
###### ✋ writable 
> <code>( _true_ | _false_ )</code>
> <code>можно ли изменять значение свойства</code>
> <code>( по умолчанию _true_ )</code>
###### ✋ set
> <code>сеттер свойства</code><br/>
> <code>( функция, которая вызывается при записи значения свойства )</code><br/>
> <code>( по умолчанию имеет значение _undefined_ )</code>
###### ✋ **get**
> <code>геттер свойства </code><br/>
> <code>( функция, которая вызывается при чтении значения свойства )</code><br/>
> <code>( по умолчанию имеет значение _undefined_ )</code>
###### ✋ **enumerable** ( `true` | `false` )
> <code>является свойство перечислимым, или нет </code><br/>
> <code>т.е. будет ли оно итерироваться оператором **_for..in_**</code><br/>
> <code>и возвращаться при вызове метода **_Object.keys()_**</code><br/>
> <code>( по умолчанию имеет значение _false_ )</code>
###### ✋ **configurable** ( `true` | `false` )
> <code>доступно ли свойство для модификации ( удаления, изменения атрибутов свойства )</code><br/>
> <code>можно ли конфигурировать свойство с помощью метода **_defineProperty_** </code><br/>
> <code>( по умолчанию _false_ )</code><br/>

```javascript
var newObject = {
    name: "Егор",
    age: 25,
    write: true,
    read: true,
    getName() {},
    setName() {}
}
Object.getOwnPropertyDescriptor ( newObject, "getName" )
```
###### Результат:
```console
▼ {value: ƒ, writable: true, enumerable: true, configurable: true}
    configurable: true
    enumerable: true
  ► value: ƒ getName()
    writable: true
  ► __proto__: Object
```

| [:arrow_double_up:](#top) |
|-|

## :mortar_board: Object.defineProperty()
###### Этот метод позволяет создать объекту свойство с дескриптором
###### Первый аргумент метода - ссылка на объект, которому добавляется свойство
###### Второй аргумент - имя свойства ( строка )
###### Третий аргумент - объект дескриптора свойства

<code>Добавим свойство <b>type</b> объекту <b>sample</b> и сделаем это свойство неперечислимым</code>
```javascript
var sample = {
    name: "figure",
    size: 100,
    color: "red"
}
Object.defineProperty ( sample, 'type', {
    value: "svg",
    enumerable: false
})

Object.keys ( sample )
```
###### Результат:
```console
► (3) ["name", "size", "color"]
```
###### геттер и сеттер свойства
<code>Добавим еще одно свойство объекту  **sample**</code><br/>
<code>Свойство   **_operation_**   будет  с геттером и сеттером</code><br/>
:warning: <code>Когда определяются атрибуты _`get()`_  и  _`set()`_ в дескрипторе свойства, </code><br/>
<code>нельзя использовать атрибуты  _`writable`_ и _`value`_</code>
```javascript
Object.defineProperty ( sample, "operation", {
    get: () => this.operation ? 
               this.operation.substr ( 0, 1 ) : "?",
    set: newVal => this.operation = newVal + "***"
})
```
###### Результат:
```console
▼ {name: "figure", size: 100, color: "red", type: "svg"}
    color: "red"
    name: "figure"
    size: 100
    operation: (...)
    type: "svg"
  ► get operation: () => {…}
  ► set operation: newVal => this.operation = newVal + "***"
  ► __proto__: Object
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