## :mortar_board: Деструктуризация
###### ES6

Деструктуризация - это разложение структуры данных на элементарные составляющие

    Структура данных - это совокупность элементов, 
    объединенных под одним именем
    и организованных по определенному принципу

    Фактически структура данных - это именованная капсюла
    с четким протоколом доступа к ее содержимому:
    в массиве - по индексу элемента массива,
    в объекте - по имени свойства

    Структуру данных можно "рассыпать" в отдельные переменные
    Это и есть деструктуризация

:warning: Как правило, при деструктуризации имеет место присваивание

    В левой части оператора присваивания 
    будет перечень переменных
    в квадратных или фигурных скобках 
    ( в зависимости от того, что деструктурируем ),
    в правой - массив или объект, 
    который мы деструктурируем

###### Массивы
* При деструктуризации массива переменные в левой части оператора присваивания должны перечисляться в **квадратных** скобках

:coffee: :one:
```javascript
const fruits = [ "банан", "апельсин", "киви" ]
let [ var1, var2, var3 ] = fruits

console.info ( var1 )   // "банан"
console.info ( var2 )   // "апельсин"
console.info ( var3 )   // "киви"
```
:coffee: :two:
###### обмен значениями между переменными 
```javascript
let x = 5, y = 7, z = 9
[ x, y, z ] = [ y, z, x ]

console.info ( x )  // 7
console.info ( y )  // 9
console.info ( z )  // 5
```

:coffee: :three:
###### Функция getArr возвращает массив
```javascript
let getArr = deg => [ Math.sin ( deg ), Math.cos ( deg ) ]
```
###### получим результат ее работы в переменные  _sin30_  и  _cos30_
```javascript
let [ sin30, cos30 ] = getArr ( Math.PI/3 )

console.info ( sin30 )  // 0.8660254037844386
console.info ( cos30 )  // 0.5
```
:coffee: :three:
###### выборка
```javascript
let getAngleData = 
    deg => [ 
        Math.sin ( deg ), 
        Math.cos ( deg ), 
        Math.tan ( deg ), 
        Math.atan ( deg ) 
    ]
```
###### Вызовем эту функцию, но "пропустим" возвращаемое ею значение тангенса угла:
```javascript
let [ sin30, cos30, , arctg30 ] = getAngleData ( Math.PI/3 )

console.info ( sin30 )  // 0.8660254037844386
console.info ( cos30 )  // 0.5
console.info ( arctg30 )  // 0.808448792630022
```

## Объекты
Если мы деструктурируем объект, то переменные в левой части оператора присваивания будут перечисляться в **фигурных** скобках

:warning: При этом имена переменных должны совпадать с именами свойств объекта<br/>
( порядок следования не имеет значения )

:coffee:
```javascript
const user = { 
    name: "Georg", 
    role: "admin", 
    stars: 5 
}

let { name, role, stars } = user

console.info ( name )   // "Georg"
console.info ( role )   // "admin"
console.info ( stars )  // 5
```
:warning: :one:

если при деструктуризации объекта переменные в левой части оператора присваивания были объявлены ранее, то все выражение нужно заключить в круглые скобки:
```javascript
let name, age

( { name, age } = { name: "Ivan", age: 25 } )
```
В противном случае будет сгенерировано исключение
```console
⛔️ Uncaught SyntaxError: Unexpected token =
```
:warning: :two:

Если мы хотим присвоить значение переменной с именем, отличающимся от имени свойства деструктурируемого объекта,
то при перечислении имен свойств в левой части оператора присваивания через двоеточие можно указать новое имя переменной:
```javascript
const user = { 
    login: "Ivan", 
    age: 42, 
    works: true
}

let { 
    login: userName,
    works: employed 
} = user 

console.log( userName )   // "Ivan"
console.log( employed )   // true
```
:warning: :three:

При деструктуризации объектов можно устанавливать значения переменных по умолчанию<br/>
( на случай, если такого свойства в объекте нет )
```javascript
let {
    login = "Сергей",
    speciality = "слесарь"
} = { login: "Ivan", age: 42 }
 
console.log( login )       // "Ivan"
console.log( speciality )  // "слесарь"
```
***
## spread ( `...` )

Оператор **`...`** позволяет получить:
* результат деструктуризации массива
* остаток от дестуктурированного массива

:coffee: :one:
###### функция  _getAngleData_  возвращает массив
```javascript
let getAngleData = 
    deg => [ 
        Math.sin ( deg ), 
        Math.cos ( deg ), 
        Math.tan ( deg ), 
        Math.atan ( deg ) 
    ]
```
###### функция  _func_  принимает 4 аргумента
```javascript
let func = ( x, y, z, w ) => {
    console.log ( x )
    console.log ( y )
    console.log ( z )
    console.log ( w )
}
```
###### Передадим результат работы функции _getAngleData_ функции _func_
```javascript
func ( ...getAngleData ( Math.PI/3 ) )

// 0.8660254037844386
// 0.5000000000000001
// 1.7320508075688767
// 0.808448792630022
```

:coffee: :two:
###### получим остаток массива, возвращаемого функцией _getAngleData_, в массив _rest30_
```javascript
let [ sin30, ...rest30 ] = getAngleData ( Math.PI/3 )

console.info ( sin30 )  // 0.8660254037844386
console.log ( rest30 )  
// (3) [0.5000000000000001, 1.7320508075688767, 0.808448792630022]
```

:coffee: :three:
###### разметка
```html
<body>
    <p class="paragraph">1</p>
    <p class="paragraph">2</p>
    <p class="paragraph">3</p>
    <p class="paragraph">4</p>
</body>
```
###### код
```javascript
let collection = document.querySelectorAll ( '.paragraph' )
let [ first, second, third, forth ] = collection
```
###### или
```javascript
let [ first, second, third, forth ] = 
    document.querySelectorAll ( '.paragraph' )
```
###### результат
```javascript
console.log ( first )   // <p class="paragraph">1</p>
console.log ( second )  // <p class="paragraph">2</p>
console.log ( third )   // <p class="paragraph">3</p>
console.log ( forth )   // <p class="paragraph">4</p>
```
***
### [:briefcase: Упражнения](https://docs.google.com/forms/d/e/1FAIpQLSeSywg6vOrnZ0JJdvqOjB9OSNT3FcBBRJox7Qt2661Nz_C8CA/viewform)