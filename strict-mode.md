# :mortar_board: strict mode
###### "use strict"
Это директива для интерпретатора, которая не позволяет ему выполнять код, если в нем есть отступления от спецификации языка<br/>
( интерпретатор будет генерировать исключение )

Директива `'use strict'` распознается только в начале скрипта или функции
```javascript
function sample () {
        'use strict'
        ...
}
```
Директива 'use strict' переводит выполнение скрипта в строгий режим ( **`strict mode`** )

### :no_entry_sign: **В этом режиме нельзя**:

#### :warning: использовать необъявленные переменные 
```javascript
'use strict'
x = 8
```
будет сгенерировано исключение: 
```
⛔️ Uncaught ReferenceError: x is not defined
```
#### :warning: удалять переменные и функции оператором  **`delete`**
###### обычный режим:
```javascript
function sum ( x, y ) {
    return x + y
}
delete sum   // false
```
###### строгий режим:
```javascript
'use strict'
function sum ( x, y ) {
    return x + y
}
delete sum
```
будет сгенерировано исключение: 
```
⛔️ Uncaught SyntaxError: 
Delete of an unqualified identifier in strict mode.
```
#### :warning: присваивать восьмеричные значения
###### обычный режим:
```javascript
var x = 010   // 8
```
###### строгий режим:
```javascript
'use strict'
var x = 010
```
будет сгенерировано исключение:
```
⛔️ Uncaught SyntaxError: 
Octal literals are not allowed in strict mode.
```
#### :warning: использовать экранированные восьмеричные значения
###### обычный режим:
```javascript
var x = "\010"   // ""
```
###### строгий режим:
```javascript
'use strict'
var x = "\010"
```
будет сгенерировано исключение:
```
⛔️ Uncaught SyntaxError: 
Octal escape sequences are not allowed in strict mode.
```
#### :warning: изменять значения неперезаписываемых свойств
###### обычный режим:
```javascript
var sample = Object.defineProperty(
    {},
    "x",
    { value:0, writable:false }
)
sample.x = 5   // 0
```
###### строгий режим:
```javascript
'use strict'
var sample = Object.defineProperty(
    {},
    "x",
    { value:0, writable:false }
)
sample.x = 5
```
будет сгенерировано исключение:
```
⛔️ Uncaught TypeError: 
Cannot assign to read only property 'x' of object '#<Object>'
```
#### :warning: изменять значения свойств с геттером ( без сеттера)
###### обычный режим:
```javascript
var obj = { 
    get x() {
        return 0
    } 
}
obj.x = 5 // 0
```
###### строгий режим:
```javascript
'use strict'
var obj = { 
    get x() {
        return 0
    } 
}
obj.x = 5
```
будет сгенерировано исключение:
```
⛔️ Uncaught TypeError: 
Cannot set property x of #<Object> which has only a getter
```
#### :warning: удалять неудаляемые свойства
###### обычный режим:
```javascript
delete Object.prototype  // false
```
###### строгий режим:
```javascript
'use strict'
delete Object.prototype
```
будет сгенерировано исключение:
```
⛔️ Uncaught TypeError: 
Cannot delete property 'prototype' of function Object() { [native code] }
```
#### :warning: использовать **_eval_** как имя переменной
###### обычный режим:
```javascript
var eval = 7  // 7
```
###### строгий режим:
```javascript
'use strict'
var eval = 7
```
будет сгенерировано исключение:
```
⛔️ Uncaught SyntaxError: 
Unexpected eval or arguments in strict mode
```
#### :warning: использовать **_arguments_** как имя переменной
###### обычный режим:
```javascript
var arguments = 7  // 7
```
###### строгий режим:
```javascript
'use strict'
var arguments = 7
```
будет сгенерировано исключение:
```
⛔️ Uncaught SyntaxError: 
Unexpected eval or arguments in strict mode
```
#### :warning: использовать выражение _**with**_ 
###### обычный режим:
```javascript
var x, y
with ( String ) {
   x = fromCharCode ( 89, 75 )
}
console.log ( x )  // "YK"
with ( Math ) {
   y = round ( x = random () * 1000 )
}
console.log ( y )  // 256
```
###### строгий режим:
```javascript
'use strict'
var x, y
with ( String ) {
   x = fromCharCode ( 89, 75 )
}
console.log ( x )  // "YK"
with ( Math ) {
   y = round ( x = random () * 1000 )
}
console.log ( y )  // 256
```
будет сгенерировано исключение:
```
⛔️ Uncaught SyntaxError: 
Strict mode code may not include a with statement
```
#### :warning: метод **_eval ()_** не может создавать переменные в области видимости, в которой он был вызван
###### по соображениям безопасности 
###### обычный режим:
```javascript
eval ( "var gamma = 2" )
console.log ( gamma )
```
###### строгий режим:
```javascript
'use strict'
eval ( "var gamma = 2" )
console.log ( gamma )
```
будет сгенерировано исключение:
```
⛔️ Uncaught ReferenceError: 
gamma is not defined
```
#### :warning: использовать как имена переменных ключевые слова:

    🔴 implements
    🔴 interface
    🔴 let
    🔴 package
    🔴 private
    🔴 protected
    🔴 public
    🔴 static
    🔴 yield

будет сгенерировано исключение:
```
⛔️ Uncaught SyntaxError: 
Unexpected strict mode reserved word
```