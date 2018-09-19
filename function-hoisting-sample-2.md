[:arrow_backward:](https://github.com/garevna/js-course/wiki/function-object#hoisting) **hoisting**

#### :coffee: 2

```javascript
var treg = 5

function delegat () {
        treg = 10
        return
        function treg (  ) {
                return
        }
}
delegat ()
console.log ( treg )  // 5
```

В этом случае объявление функции  **`treg`**  попадет в *Lexical Environment* функции  **`delegat`** на этапе создания ее контекста выполнения, и не затронет переменную  **`treg`**,  объявленную в глобальном контексте

Это будут разные переменные,  хотя идентификаторы у них совпадают

Поэтому  в результате в консоли будет **5**

[:arrow_backward:](https://github.com/garevna/js-course/wiki/function-object#hoisting) **hoisting**