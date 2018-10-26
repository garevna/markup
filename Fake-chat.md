## :briefcase: Fake chat

### :clipboard: db.json
Внесем некоторые изменения в базу данных **db.json**

###### :pencil2: lastUpdate
`Добавим запись `**_`lastUpdate`_**` с двумя полями:`
```javascript
"lastUpdate": {
    "data": "26.10.2018",
    "time": "12:38:01"
}
```
`Мы будем использовать эти данные для обновления чата`<br/>
`после того, как данные в  `**`db.json`**`  были обновлены`<br/>
`( операции POST | PUT | DELETE )`

###### :pencil2: posts
`В каждую запись базы данных `**`posts`**` добавим свойства `**`date`**` и `**`time`**`
```javascript
"posts": [
    {
      "id": 0,
      "date": "05.08.2018",
      "time": "10:30:15",
      "userId": 2,
      "title": "My first post here",
      "body": "It's really wonder!"
    },
    ...
}
```
***
### :clipboard: json-server

<img src="https://github.com/garevna/js-course/blob/master/images/git-bush-ico.png" width="25"/> Запускаем  json-server
```console
json-server --watch db.json
```
Получаем **endpoints**:
```console
Resources
        http://localhost:3000/lastUpdate
        http://localhost:3000/users
        http://localhost:3000/posts
        http://localhost:3000/comments

Home
        http://localhost:3000
```
***
* Открываем в браузере страницу **http://localhost:3000**
* заходим в _Chrome DevTools_
* Создаем  snippet

<a name="snippet"></a>

| vars | functions |  |
|-|-|-|
| [`lastUpdate`](lastUpdate) | [`getData`](getData) |  |
| [`chat`](vars) | [`appelem`](appelem) |  |
| [`posts`](vars) | [`buildChat`](buildChat) |  |
| [`users`](vars) | [`initChat`](initChat) |  |
| [`currentUser`](vars) | [`updateChat`](updateChat) |  |
| [`chatInput`](chatInput) | [`Запуск`](#clipboard-%D0%97%D0%B0%D0%BF%D1%83%D1%81%D0%BA) |  |

###### 
`Объявляем переменную `**_`lastUpdate`_**`,`<br>`в которой будем хранить дату и время модификации загруженных данных`
```javascript
let lastUpdate
```
###### getData
`Объявляем переменную `**_`getData`_**`,`<br/>
`в которой будет ссылка на функцию, загружающую данные с сервера`<br/>
`по имени ресурса ( `**_`lastUpdate`_**`, `**_`users`_**`, `**_`posts`_**`, `**_`comments`_**` )`
```javascript
let getData = function ( ref ) {
    return fetch ( 'http://localhost:3000/' + ref )
        .then ( response => response.json () )
}
```
###### appElem

`Объявляем переменную `**_`appElem`_**<br/>
`В этой переменной будет ссылка на анонимную стрелочную функцию`<br/>
`Функция получает в первом аргументе имя тега `**_`tagName`_**,<br/>
`и создает элемент DOM`<br/>
`Второй ( опциональный ) аргумент `**_`container`_** `может содержать ссылку`<br/>
`на элемент-контейнер, куда нужно вставить созданный элемент`<br/>
`Если такой аргумент отсутствует, то функция вставляет элемент`<br/>
`в `_`document.body`_
```javascript
let appElem = ( tagName, container ) => 
    ( container ? container : document.body )
        .appendChild (
            document.createElement ( tagName )
        )
```
<a name="vars"></a>
###### chat
`ссылка на элемент DOM, который будет контейнером для сообщений чата`
###### posts & users
`В переменные posts и users будем получать данные из базы данных на сервере`
###### currentUser
`объект активного пользователя чата ( от лица которого мы будем писать в чат )`

```javascript
let chat
let posts
let users

let currentUser
```
###### chatInput
`Создаем элемент input ( поле для ввода текста сообщения )`<br/>
`и стилизуем элемент:`
```javascript
let chatInput = appElem ( 'input' )
chatInput.style = `
    position: fixed;
    left: 20px;
    width: 80%;
    bottom: 10px;
    border: inset 1px;
    background-color: #af9;
    overflow: auto;
`
```
###### buildChat
`Ссылка на функцию, создающую элемент section ( это будет чат )`
```javascript
let buildChat = function () {
    chat = appElem ( 'section' )
    chat.style = `
        position: fixed;
        top: 30px;
        left: 20px;
        right: 20px;
        bottom: 70px;
        border: inset 1px;
        overflow: auto;
        padding: 10px;
    `
}
```
###### initChat
`Ранее мы уже объявили переменную `**`chat`**

`После вызова функции `**`buildChat`**<br/>
`в этой переменной ( `**`chat`**` ) будет ссылка на элемент `**`section`**`,`<br/>
`который будет контейнером для сообщений в чате`

`Асинхронная функция `**`initChat`**` будет итерировать массив `**`post`**<br/>
`с помощью метода `**`forEach`**<br/>
`заполнять контейнер `**`chat`**` данными из массива `**`post`**<br/>
`( данные к моменту вызова функции должны быть уже получены от сервера )`

`В первую очередь контейнер `**`chat`**` освобождается:`
```javascript
chat.innerHTML = ""
```
`На каждой итерации по значению `**`post.userId`**<br/>
`находится соответствующий элемент массива `**`users`**<br/>
`( с помощью метода  `**`filter`**` )`

`На каждой итерации создается элемент div,`<br/>
`который будет контейнером для очередной записи`<br/>
`из массива `**`post`**

`Для создания новых элементов DOM  и вставки их на страницу `<br/>
`используем асинхронную функцию `**`appElem`**
```javascript
let initChat = async function () {
    chat.innerHTML = ""
    posts.forEach ( post => {
        let user = users.filter (
            x => x.id === post.userId 
        )[0]
        chat.appendChild (
            ( function () {
                let cont = appElem ( 'div' )
                let ava = appElem ( 'img', cont )
                ava.src = user.photoURL
                ava.width = "40"
                ava.title = ` ${user.name} ${user.lastName}`
                appElem ( 'span', cont ).innerHTML = 
                    ` <small> ${post.date} ${post.time}</small>`
                appElem ( 'p', cont ).innerText = post.body
                return cont
            }) ( user )
        )
    })
}
```
###### updateChat
`Объявляем переменную `**`updateChat`**`,<br/>
`в которую помещаем ссылку на асинхронную анонимную функцию `**`updateChat`**

`✋ Используем функцию `**`getData`**` для получения даты и времени<br/>
`последнего обновления базы данных`<br/>
`в переменную `**`updated`**`,`<br/>
`используя ключевое слово `**_`await`_**`,`<br/>
`чтобы дождаться результата асинхронной операции`

`✋ Сравниваем дату и время обновления загруженных данных`<br/>
`с датой и временем последнего обновления базы данных`<br/>
`Если загруженные данные актуальны`<br/>
`( после их загрузки обновлений базы данных не было ),`<br/>
`то завершаем выполнение функции `**`updateChat`**` ( `*`return`*` )`

`✋ В противном случае формируем массив промисов:`
```javascript
[ 
    getData ( "users" ).then ( x => users = x ) , 
    getData ( "posts" ).then ( x => posts = x ) 
]
```
`и передаем его методу `**`Promise.all`**`,`<br/>
`который также вызываем с ключевым словом `**_`await`_**

`✋ Когда `**_`Promise.all`_**`  будет разрешен, проверяем, есть ли значение`<br/>
`у объявленной ранее переменной `**`currentUser`**<br/>
`( пользователь, от лица которого будут добавляться сообщения в чат )`<br/>
`Если активный пользователь еще не определен,`<br/>
`выбираем его случайным образом из числа всех зарегистрированных пользователей ( `**`users`**` )`

`✋ Вызываем функцию `**`initChat ()`**
```javascript
let updateChat = async function () {
    let updated = await getData ( "lastUpdate" )
    if ( lastUpdate && updated.data === lastUpdate.data && 
        updated.time === lastUpdate.time ) return

    let scrollValue = chat.scrollTop

    await Promise.all ( [ 
        getData ( "users" ).then ( x => users = x ) , 
        getData ( "posts" ).then ( x => posts = x )
    ] )

    if ( !currentUser ) {
        currentUser = users [
            Math.floor ( Math.random () * users.length )
        ]
        currentUserId = currentUser.id
    }

    initChat ()
    chat.scrollTop = scrollValue
}
```
`Свойство `**_`scrollTop`_**` можно использовать для управления прокруткой чата`<br/>
`Если установить`
```javascript
chat.scrollTop = chat.offsetTop
```
`то элемент `**`chat`**` будет прокручен до конца`<br/>
`( мы будем видеть последние сообщения в чате )`
***
### :clipboard: Запуск

* вызваем **buildChat ()**, чтобы создать контейнер для чата
* вызваем **updateChat ()**, чтобы заполнить контейнер данными
* устанавливаем интервал обновления чата ( **setInterval** )
```
через заданные интервалы времени 
мы будем вызывать updateChat (),
чтобы проверить, было ли за это время
обновление базы данных на серевере,
и если да - обновлять 
содержимое чата на клиенте
```
* вешаем обработчика события **change** элемента **chatInput**
```
если клиент введет сообщение, это сообщение нужно
отправить на сервер для добавления в базу данных
```
Итак:
```javascript
buildChat ()
updateChat ()

setTimeout ( function () {
    chat.scrollTop = chat.scrollHeight
}, 100 )

let interval = setInterval ( function () {
    updateChat ()
}, 1000 )

chatInput.onchange = function ( event ) {
    let postTime = new Date().toLocaleString ().split ( ', ' )
    fetch ( 'http://localhost:3000/posts', {
        method: 'POST',
        body: JSON.stringify ({
            date: postTime [0],
            time: postTime [1],
            userId: currentUserId,
            body: event.target.value
        }),
        headers: {
            "Content-type": "application/json"
        }
    })
}
```
***
[:page_with_curl: **Полный код сниппета**](fake-chat-snippet)