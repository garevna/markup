## :briefcase: Fake chat

### db.json

Внесем некоторые изменения в базу данных **db.json**

###### :pencil2: lastUpdate
Добавим запись **_lastUpdate_** с двумя полями:
 
✅ **data**  
✅ **time**

Мы будем использовать эти данные для обновления чата<br/>
после того, как данные в  **db.json**  были обновлены<br/>
`( операции POST | PUT | DELETE )`

###### :pencil2: posts
В каждую запись базы данных **posts** добавим свойства

✅ **data**  
✅ **time**

### json-server

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

### snippet

Создаем сниппет в Chrome DevTools
###### lastUpdate
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
###### initChat
Ранее мы уже объявили переменную  chat

После вызова функции  buildChat
в этой переменной ( chat ) будет ссылка на элемент section,
который будет контейнером для сообщений в чате

Функция  initChat  будет итерировать массив post
с помощью метода  forEach
и заполнять контейнер  chat  данными из массива post
( данные к моменту вызова функции должны быть 
уже получены от сервера )

В первую очередь контейнер  chat  освобождается:
chat.innerHTML = ""

На каждой итерации по значению post.userId
находится соответствующий элемент массива users
( с помощью метода  filter )

На каждой итерации создается элемент div,
который будет контейнером для очередной записи
из массива post

Для создания новых элементов DOM  и вставки их на страницу 
мы используем функцию appElem
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