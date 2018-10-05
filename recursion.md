## :mortar_board: Рекурсия

Рекурсия - это процесс, в котором функция вызывает сама себя, прямо или косвенно

⚠️ Каждая рекурсивная функция должна иметь условие прерывания рекурсии

В противном случае вызов функции приведет к бесконечному циклу

**Хвостовая рекурсия** - это когда последним исполняемым оператором рекурсивной функции будет оператор  **_return_** с вызовом этой же функции

Простейший ( классический ) пример рекурсии - вычисление факториала

:coffee: :one:
```javascript
function factorial ( num, result ) {
   result = ( !result ? 1 : res ) * num--
   return num < 2 ? result : factorial ( num, result )
}
```
:coffee: :two:
```javascript
function factorial ( n, result = 1 ) {
   result *= n--
   return n < 2 ? result : factorial ( n, result )
}
```

:coffee: :three:
```javascript
function factorial ( n, result ) {
   while ( n > 1 )
      return factorial ( n - 1, n * ( !result ? 1 : result ) )
   return result
}
```

:coffee: :four:
```javascript
function factorial ( n, result ) {
   return n < 2 ? !result ? 1 : result :
       factorial ( n- 1, n * ( !result ? 1 : result ) )
}
```

:coffee: :five:

Для того, чтобы избавиться от опционального параметра, используем замыкание:
```javascript
function factor ( num ) {
   var res = 1
    return ( function fact () {
       res *= num
       return num < 2 ? res : fact ( --num )
    })()
}
```

В JavaScript каждый вызов функции добавит кадр вызова в стек

Когда вызов завершается, кадр удаляется из стека

Однако рекурсивная функция не завершается сразу

Она вернет рекурсивный вызов самой себя

Это будет каждый раз добавлять в стек контекст функции

Если хвостовая рекурсия достаточно глубокая, это может привести к переполнению стека и генерации исключения  **`RangeError`**

>> Исключение **`RangeError`** возникает тогда, когда глубина рекурсии превышает 10000

:briefcase: Упражнение

Разберите код функции circle
```javascript
var circle = function ( radius ) {
        var elem = document.createElement ( "div" )
        document.body.appendChild ( elem )
        elem.style = `
             position: absolute;
             width: ${radius}px;
             height: ${radius}px;
             border-radius: 50%;
             border: solid 1px green;
        `
        if ( radius < 300 ) circle ( radius += 20 )
}
```
Вызовите функцию circle