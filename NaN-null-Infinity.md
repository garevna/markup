[Infinity]: https://github.com/garevna/js-course/wiki/NaN-null-Infinity#-%D0%97%D0%BD%D0%B0%D1%87%D0%B5%D0%BD%D0%B8%D0%B5-infinity
[null]: https://github.com/garevna/js-course/wiki/NaN-null-Infinity#-%D0%97%D0%BD%D0%B0%D1%87%D0%B5%D0%BD%D0%B8%D0%B5-null
[NaN]: https://github.com/garevna/js-course/wiki/NaN-null-Infinity#-%D0%97%D0%BD%D0%B0%D1%87%D0%B5%D0%BD%D0%B8%D0%B5-nan

| [:arrow_down: null][null] | [:arrow_down: Infinity][Infinity] |
|-|-|
***
# 🎓 Значение NaN

`📌 Тип данных  "number"`

Сокращение от  "**Not a Number**" ( результат операции не является числом )

Можно получить в результате приведения типов, например:
```javascript
     5 / "a"  --> NaN
     "b" * 3  --> NaN
```
`NaN` является свойством глобального объекта ( `window` )

`NaN` также является свойством встроенного объекта  `Number`

⚠️ `NaN` не равен ничему, даже самому себе 
```javascript
     NaN === NaN            // false
     NaN == NaN             // false
     NaN >= NaN             // false
     NaN <= NaN             // false
```
Для определения, является ли значением выражения `NaN`, 

можно использовать методы   `isNaN ()`  и  `Number.isNaN ()`

Их действие не идентично
```javascript
isNaN ( "привет" )               //  true
Number.isNaN ( "привет" )        //  false
Number.isNaN ( "привет" / 10 )   //  true
```
> :hash: `isNaN ()`  возвращает `true`, если после приведения типа аргумента к числу результат будет  `NaN`

> :hash: `Number.isNaN ()`  возвращает `true`, если аргумент имеет значение  `NaN`  ( приведения типа не происходит )

# 🎓 Значение null

`📌 Тип данных  "object"`

### 📖 null 

>Специальное значение `null` означает "ничего"

⚠️ `null` может равняться только `null` или ( при нестрогом сравнении ) `undefined`

```javascript      
null == null              // true
null === null             // true
null == undefined         // true
null === undefined        // false
null == 0                 // false
null == NaN               // false
null == false             // false
null == ""                // false
null == []                // false
```

[:arrow_heading_up:][NaN]

# 🎓 Значение Infinity

`📌 Тип данных  "number"`

Значение, превышающее максимально возможное число с плавающей  запятой

Максимально возможное число с плавающей  запятой:

`1.7976931348623157E+10308`

Может быть отрицательным ( `-Infinity` )

`Infinity` может быть результатом деления на ноль отличного от нуля числа
```javascript
1 / 0            //  Infinity
```
Однако:
```javascript
0 / Infinity  // NaN

Infinity / Infinity  // NaN
Infinity - Infinity  // NaN

Infinity * Infinity  // Infinity
Infinity + Infinity  // Infinity
```
***
| [:arrow_heading_up: NaN][NaN] | [:arrow_heading_up: null][null] |
|-|-|
***
[🔗 w3schools](https://www.w3schools.com/jsref/jsref_infinity.asp)