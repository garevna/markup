[:arrow_backward:](function-object#callee) **arguments.callee**

#### :coffee: 5

В этом примере создаются анонимные функции, которые обрабатывают событие **`click`**  кнопок

Каждая функция "накапливает" данные о времени клика на кнопке в массиве **`arguments.callee.res`**

```javascript
var buttons = []
for ( var n = 0; n < 5; n++ ) {
    buttons [ n ] = document.body.appendChild ( 
          document.createElement( 'button' ) 
    )
    buttons [ n ].innerText = n
    buttons [ n ].onclick = function ( event ) {
       if ( !arguments.callee.res )
             arguments.callee.res = []
       arguments.callee.res.push ( event.timeStamp )
             console.log ( arguments.callee.res )
    }
}
```

Модифицируем этот код:

```javascript
var buttons = []
for ( var n = 0; n < 5; n++ ) {
    buttons [ n ] = document.body.appendChild ( 
             document.createElement( 'button' ) 
    )
    buttons [ n ].innerText = n
    buttons [ n ].onclick = function ( event ) {
        if ( !arguments.callee.clicksTime )
            arguments.callee.clicksTime = []
        arguments.callee.clicksTime.push ( event.timeStamp )
        console.log ( arguments.callee.clicksTime )
        arguments.callee.res = arguments.callee.clicksTime.length > 1 ? 
            arguments.callee.clicksTime [ arguments.callee.clicksTime.length - 1 ] -
            arguments.callee.clicksTime [ arguments.callee.clicksTime.length - 2 ] : 0

        console.info ( `Интервал между последними кликами: ${arguments.callee.res}` )
    }
}
```

Что теперь делает каждый обработчик клика на кнопке ?

[:arrow_backward:](function-object#callee) **arguments.callee**