## 📖 Оператор ```typeof```

Возможные значения, возвращаемые оператором ```typeof```:
```javascript
        ✅ "string"
        ✅ "number"
        ✅ "boolean"
        ✅ "object"
        ✅ "undefined"
        ✅ "function"
```
Оператор  ```typeof```  возвращает строку

### ☕

✍️ Наберите в консоли:

```javascript
var x = 10
typeof x
```
```javascript
    // в консоль будет выведено   "number"
```
✍️ А теперь выполните код в консоли:

```javascript
x = "google"
typeof x
```
```javascript
    // в консоль будет выведено   "string"
```
✍️ Теперь выполните в консоли следующий код:

```javascript
var x = 10
typeof typeof x
```
```javascript
    // в консоль будет выведено   "string"
```
## 📖 string

Строки состоят из символов и заворачиваются в двойные ( *"мама"* ) или одинарные ( *'мама'* ) кавычки

Также можно завернуть строку в обратные кавычки ``` ` ```
```javascript
var sample = `This is a sample`
```
Если внутри строки встречаются двойные кавычки, то сама строка должна быть завернута в одинарные, и наоброт

>☕
```javascript
var first = 'Капитаном корабля "Наутилус" был Немо'
var second = "Капитаном корабля 'Наутилус' был Немо"
var third = `Капитаном корабля "Наутилус" был Немо`
```

## 📖 number

Число может быть:
```javascript
     ✅ целым ( 5 )
     ✅ с плавающей точкой ( 5.80 )
     ✅ Infinity ( бесконечность ) 
     ✅ NaN ( Not a Number - не число )
```
>✋ Значение *Infinity*  может получиться при делении на ноль:
```javascript
var x = 1, y = 0
var z = x / y
```
Значением переменной  z  будет  *Infinity*

>✋ Значение *NaN* может получиться при попытке выполнения арифметических операций с операндами, которые не являются числами, например:   ``` 5 * "total" ```, а так же при попытке разделить ноль на ноль: ``` 0/0 ```

>>⚠️ Значение   *NaN*  не равно никакому другому значению, включая само значение *NaN*

>>⚠️ Никакие арифметические операции в JS никогда не будут завершены с ошибкой, поскольку в случае ошибки операция вернет *NaN*

## 📖 boolean

Логический тип

Данные логического типа могут принимать только одно из двух значений: 

    ✅ true ( истина ) 
    ✅ false ( ложь )

## 📖 object

К данным типа object относятся:
```javascript
        ✅ объекты
        ✅ массивы
        ✅ null
```

### 📖 null 

>Специальное значение ```null``` означает "ничего"

⚠️ ```null``` может равняться только ```null``` или ( при нестрогом сравнении ) ```undefined```

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

## 📖 Массивы

Массив - это упорядоченный набор данных ( *структура данных* )

    ✋ Каждый элемент массива имеет порядковый номер ( индекс элемента массива )
    ✋ Нумерация элементов в массиве начинается с 0
    ✋ Получить элемент массива можно по его индексу

Запись массива в JS очень проста: элементы массива перечисляются через запятую в квадратных скобках:

     [ 15, 50, 78 ]

Каждый элемент массива может иметь собственный тип данных, отличный от типов других элементов массива

☕ 1
```javascript
var  numbers = [ 1, 5, 78 ]
```
```javascript
    // Значение    numbers [ 0 ]     будет     1
    // Значение    numbers [ 1 ]     будет     5
    // Значение    numbers [ 2 ]     будет     78
```
☕ 2
```javascript
var  students = [ "Николай", "Сергей", "Иван" ]
```
```javascript
    // Значение    students [ 0 ]     будет     "Николай"
    // Значение    students [ 1 ]     будет     "Сергей"
    // Значение    students [ 2 ]     будет     "Иван"
```
☕ 3
```javascript
var  person = [ "Николай", true, 25 ]
```
```javascript
    // Значение    person [ 0 ]     будет     "Николай"
    // Значение    person [ 1 ]     будет     true
    // Значение    person [ 2 ]     будет     25
```

## 📖 undefined

Специальный тип данных, означающий, что значение переменной не определено

☕
```javascript
var  sample
console.log ( sample )
```
```javascript
    // В консоль будет выведено undefined, 
    // поскольку мы не присвоили переменной  sample  
    // никакого значения
```

***

## [💼 Упражнения](https://docs.google.com/forms/d/e/1FAIpQLSfjTMY7jF_kLLHzrE5bwhxOX7gUpbZ-M3mNv9fdFVvkf3K0Tg/viewform)

***

[🔗 MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)