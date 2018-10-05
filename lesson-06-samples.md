:coffee: :one:

[:link: Перейдите по ссылке](https://developer.mozilla.org/en-US/docs/Web/API/Window/location?name=garevna,date=10.07.2018)

В консоли новой вкладки выполните код:
```javascript
location.search.slice(1).split(',')
        .map ( x => Object.assign ( {}, 
                        { [ x.split( '=' )[0] ] : x.split( '=' )[1] } 
                    ) 
        )
```
:coffee: :two:

[:link: Перейдите по ссылке](https://developer.mozilla.org/en-US/docs/Web/API/Window/location?name=garevna,date=10.07.2018)

Теперь в консоли новой вкладки объявите функцию:
```javascript
function getSearchObject () {
        var obj = {}
        location.search.slice(1).split( ',' )
                .map ( x => x.split( '=' ) )
                .map ( function ( item ) {
                        this[ item [0] ] = item [1]
        }, obj )
        return obj
}
```
Вызовите функцию  getSearchObject ()

| [:coffee::three:](https://garevna.github.io/js-samples/?name=garevna,date=10.07.2018#11 "Пример в песочнице") |
|-|
