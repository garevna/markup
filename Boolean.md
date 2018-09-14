# 🎓 Логические выражения

## 📖 Логические значения

<table>
  <tr>
    <td width="5%">
       <a href = "#-var">
          :arrow_heading_up:
       </a>
    </td>
    <td width="800">
       &nbsp;
    </td>
    <td width="5%">
       <a href = "#-%D0%9B%D0%BE%D0%B3%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D0%B5-%D0%BE%D0%BF%D0%B5%D1%80%D0%B0%D1%86%D0%B8%D0%B8">
          :arrow_heading_down:
       </a>
    </td>
  </tr>
</table>

Логических значений всего два:  **true** (истина)  и  **false**  (ложь)

## 📖 Операторы сравнения

Сравнивают две переменных ( или два выражения ) и возвращают логическое значение

| Оператор | Описание |
|:-:|:-|
| **==** | `нестрогое равенство  ( равенство значений )` |
| **===** | `строгое равенство ( равенство значений и типов данных )` |
| **!=** | `нестрогое неравенство ( значения не равны )` |
| **!==** | `строгое неравенство ( сравниваются не только  значения, но и типы данных )` |
| **>** | `больше` |
| **<** | `меньше` |
| **>=** | `больше или равно` |
| **<=** | `меньше или равно` |

:coffee:
```javascript
    var x = 5
//  Выражение	          Результат
    x == 8	           //  false	
    x == 5	           //  true
    x == "5"	           //  true
    x === 5	           //  true
    x === "5"	           //  false
    x != 8	           //  true
    x !== 5	           //  false
    x !== "5"	           //  true
    x !== 8	           //  true
    x > 8	           //  false
    x < 8	           //  true
    x >= 8                 //  false
    x <= 8                 //  true
```

## 📖 Логические операции

<table>
  <tr>
    <td width="5%">
       <a href = "#-%D0%9B%D0%BE%D0%B3%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D0%B5-%D0%B7%D0%BD%D0%B0%D1%87%D0%B5%D0%BD%D0%B8%D1%8F">
          :arrow_heading_up:
       </a>
    </td>
    <td width="800">
       &nbsp;
    </td>
    <td width="5%">
       <a href = "#-%D0%9B%D0%BE%D0%B3%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D0%B5-%D0%B2%D1%8B%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F-1">
          :arrow_heading_down:
       </a>
    </td>
  </tr>
</table>

✅ Логическое "ИЛИ"  ( || )

✅ Логическое "И"  ( && )

✅ Логическое "НЕ"  ( ! ) ( отрицание )

### 📖 &&

логическое "*И*"
```javascript
✅ true  && true    -->    true
✅ true  && false   -->    false
✅ false && true    -->    false
✅ false && false   -->    false
```

:coffee: 
```javascript
    5 > 8 && 4 < 5   // -->    false  
    // explanation: 
    5 > 8            // -->    false,
    4 < 5            // -->    true,
    false && true    // -->    false
```
:coffee: 
```javascript
    8 > 5 && 4 < 5   // -->    true
    // explanation:
    8 > 5            // -->    true,
    4 < 5            // -->    true,
    true && true     // -->    true
```

:coffee: 
```javascript
    var    x = 4,    y = 10,    z = 8
    x > y && z < y   // -->    false
    // explanation:
    x > y            // -->    false,
    z < y            // -->    true,
    false && true    // -->    false
```
:coffee: 
```javascript
    x < y && z < y   // -->    true
    // explanation:
    x < y            // -->    true,
    z < y            // -->    true,
    true && true     // -->    true
```

### 📖 ||

логическое "*ИЛИ*"
```javascript
✅ true  || true    -->    true
✅ true  || false   -->    true
✅ false || true    -->    true
✅ false || false   -->    false
```

:coffee: 
```javascript
    5 > 8 || 4 < 5   // -->    true
    // explanation:
    5 > 8            // -->    false,
    4 < 5            // -->    true,
    false || true    //  -->   true
```
:coffee: 
```javascript
    5 > 8 || 4 > 5   // -->    false
    // explanation:
    5 > 8            // -->    false,
    4 > 5            // -->    false,
    false || false   // -->    false
```
:coffee: 
```javascript
    var  x = 4,  y = 10,  z = 8
    x > y || z < y   // -->    true
    // explanation:
    x > y            // -->    false,
    z < y            // -->    true,
    false || true    // -->    true
```
:coffee: 
```javascript
    x > y || z > y   // -->    false
    // explanation:
    x > y            // -->    false,
    z > y            // -->    false,
    false || false   // -->    false
```
### 📖 !

*Логическое отрицание*
```javascript
✅ ! true   // -->   false
✅ ! false  // -->   true
```
:coffee: 
```javascript
    !(5 > 8)   // -->    true
    // explanation:
    5 > 8      // -->    false,
    !false     // -->    true
```
:coffee: 
```javascript
    !(5 > 4)   // -->    false
    // explanation:
    5 > 4      // -->    true,
    !true      // -->    false
```
✋ для логических значений x, а так же значений **null**, **NaN**, **undefined**
```javascript
    x || !x    // всегда  true
```
✋ для логических значений x
```javascript
    x && !x    // всегда  false
```
:coffee: 1
```javascript
    var x = undefined
    var y = x || !x       // -->  true
    var z = x && !x       // -->  undefined
```
:coffee: 2
```javascript
    var x = null
    var y = x || !x       // -->  true
    var z = x && !x       // -->  null
```
:coffee: 3
```javascript
    var x = NaN
    var y = x || !x       // -->  true
    var z = x && !x       // -->  NaN
```
:coffee: 4
```javascript
    var x = 5
    var y = x || !x       // -->  5
    var z = x && !x       // -->  false
```
:coffee: 5
```javascript
    var x = "h"
    var y = x || !x       // -->  "h"
    var z = x && !x       // -->  false
```
:coffee: 6
```javascript
    var x = ""   ( пустая строка )
    var y = x || !x       // -->  true
    var z = x && !x       // -->  ""
```
:coffee: 7
```javascript
    var  x = 4,  y = 10

    !( x > y )   // -->    true
    // explanation:
    x > y        // -->    false,
    !( false )   // -->    true
```

## 📖 Логические выражения

Логические выражения - это конструкции из переменных и/или констант, связанных между собой операторами сравнения и/или логическими операторами

Логические выражения принимают значения **true** или **false**

:coffee: Примеры логических выражений
```javascript
    x >= y
    z == t
    z === t
    y != x  // значение y не равно значению x
    y !== x // или значение y не равно значению x,
            // или тип данных y не совпадает с типом данных x

    y != x 
    y !== x

    x > 8 && y === 5
    typeof x === "number" || x === null
    !x === y
```
***

## [💼 Упражнения](https://docs.google.com/forms/d/e/1FAIpQLSexcuOpJS2d0KNNU1qTUlD5Exnf0FGI9Wb9d2I5YvViwuSKDA/viewform)
***
[🔗 w3schools](https://www.w3schools.com/js/js_comparisons.asp)