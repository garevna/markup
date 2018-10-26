# :mortar_board: async | await 
###### ES7

Иногда в нашем коде инициирутся асинхронные операции, результат которых необходим для работы дальнейшего кода

В таком случае необходимо приостановить выполнение кода до завершения асинхронных операций и получения нужных данных

Для этого нужно объявить асинхронную функцию ( с ключевым словом **`async`** перед **_function_** ), 
а в теле функции перед каждым выражением, возвращающим промис, поставить ключевое слово  **`await`**

Ключевое слово **`async`** используется для определения асинхронной функции

Результатом будет объект класса **AsyncFunction**

```javascript
async function test () {}
console.dir ( test )
```
```console
▼ async ƒ test()
    arguments: (...)
    caller: (...)
    length: 0
    name: "test"
  ▼ __proto__: AsyncFunction
        arguments: (...)
        caller: (...)
      ► constructor: ƒ AsyncFunction()
        Symbol(Symbol.toStringTag): "AsyncFunction"
      ▼ __proto__: ƒ ()
        ► apply: ƒ apply()
          arguments: (...)
        ► bind: ƒ bind()
        ► call: ƒ call()
          caller: (...)
        ► constructor: ƒ Function()
          length: 0
          name: ""
        ► toString: ƒ toString()
        ► Symbol(Symbol.hasInstance): ƒ [Symbol.hasInstance]()
        ► get arguments: ƒ ()
        ► set arguments: ƒ ()
        ► get caller: ƒ ()
        ► set caller: ƒ ()
        ► __proto__: Object
```
:warning: **AsyncFunction** не является глобальным объектом

Попытка отратиться к объекту **AsyncFunction** вызовет исключение:
```javascript
test instanceof AsyncFunction
```
###### :no_entry_sign:` Uncaught ReferenceError: AsyncFunction is not defined`

поэтому получить ссылку на нее можно, например, так:
```javascript
var AsyncFunctionConstructor = test.__proto__.constructor
```
или:
```javascript
var AsyncFunction = ( async function () {} ).__proto__.constructor
```
Теперь исключения не будет:
```javascript
test instanceof AsyncFunction  // true
```
:warning: Асинхронная функция всегда возвращает промис

> Поэтому нельзя конструктор объявить как асинхронную функцию - конструктор должен возвращать экземпляр объекта, а не обещание

***
### :mortar_board: Принцип работы

Ключевое слово  **`await`**  приостанавливает выполнение кода 
до завершения  асинхронной операции, запущенной выражением, следующим за  **`await`**

:warning: Ключевое слово  **`await`**  можно использовать только внутри асинхронных функций<br/>
В противном случае будет сгенерировано исключение
```console
⛔️ Uncaught SyntaxError: await is only valid in async function
```

####

Предположим, мы загружаем данные с сервера из нескольких JSON-файлов

Эти данные нужны для построения страницы, чем и занимается дальнейший скрипт

В этом случае мы обычно вешаем коллбэки с помощью метода  **then**  промисов<br/>
Если промисов много, мы выстраиваем цепочку промисов...<br/>
В общем, наш код становится громоздким<br/>

С помощью асинхронных функций мы синхронизируем асинхронные процессы<br/>
Ключевое слово  **await**  заставляет код остановится и дождаться, когда следующий за этим словом асинхронный вызов ( промис ) будет завершен с тем или иным результатом

:coffee: :one:
```javascript
async function getUsersData () {
    var promises = [
        fetch ( 'https://api.github.com/users/josh' ).then ( response => response.json() ),
        fetch ( 'https://api.github.com/users/heff' ).then ( response => response.json() ),
        fetch ( 'https://api.github.com/users/roland' ).then ( response => response.json() )
    ]
    return await Promise.all( promises )
}

getUsersData().then ( users => console.log ( users ) )
```
:coffee: :two:
```javascript
async function getUsersData ( userName ) {
    var userData = await fetch ( `https://api.github.com/users/${userName}` )
        .then ( response => response.json() )
    var userRepos = await fetch ( userData.repos_url )
        .then ( response => response.json() )
    return userRepos
}

getUsersData( 'josh' ).then ( repos => console.log ( repos ) )
```