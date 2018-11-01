## :coffee: JSON server

### :open_file_folder: Установка пакета

```console
npm install -g json-server
```

### :package: База данных

Создадим папку ( например, **_test_** ) и поместим в нее файл  **db.json**:
###### db.json
```javascript
{
    "users": [
        {
            "id": 1,
            "name": "Владимир",
            "lastName": "Кононенко",
            "email": "vladimir.kononenko@gmail.com",
            "photoURL": "https://cdn.pixabay.com/photo/2016/03/31/19/58/avatar-1295429_960_720.png"
        },
        {
            "id": 2,
            "name": "Никита",
            "lastName": "Терещенко",
            "email": "nikita.tereshenko@gmail.com",
            "photoURL": "https://i.pinimg.com/originals/3d/47/4f/3d474f82ff71595e8081f9a120892ae8.gif"
        },
        {
            "id": 3,
            "name": "Tim",
            "lastName": "Wagner",
            "email": "timVagner@gmail.com",
            "photoURL": "https://vignette.wikia.nocookie.net/yogscast/images/8/8a/Avatar_Turps_2015.jpg"
        },
        {
            "id": 4,
            "name": "James",
            "lastName": "Bond",
            "email": "jamesBond@gmail.com",
            "photoURL": "https://vignette2.wikia.nocookie.net/yogscast/images/5/59/Avatar_Lewis_2015.png"
        }
    ],
    "posts": [
        {
            "userId": 2,
            "title": "My first post here",
            "body": "It's really wonder!",
            "id": 1
        },
        {
            "postId": 2,
            "id": 2,
            "title": "Автопробег",
            "body": "Завтра планируется автопробег. Участвовать могут все желающие"
        },
        {
            "userId": 2,
            "title": "*Бетономешалка",
            "body": "Это жесть. Собираюсь купить. Лучше, чем АК!",
            "id": 3
        },
        {
            "id": 4,
            "userId": 3,
            "title": "JS",
            "body": "Look here - there are some samples"
        },
        {
            "userId": 3,
            "title": "XMLHttpRequest",
            "body": "Method POST",
            "id": 8
        }
    ],
    "comments": [
        {
            "postId": 0,
            "id": 0,
            "userId": 1,
            "body": "wow!"
        },
        {
            "postId": 0,
            "id": 1,
            "userId": 2,
            "body": "Hi, I'm wonder!"
        },
        {
            "postId": 1,
            "id": 2,
            "userId": 3,
            "body": "It's really wonder!"
        },
        {
            "postId": 2,
            "id": 3,
            "userId": 2,
            "body": "Ударим автопробегом по бездорожью и разгильдяйству!"
        }
    ]
}
```
### <img src="https://github.com/garevna/js-course/blob/master/images/git-bush-ico.png" width="25"/> Запуск сервера

Перейдем в Bush и запустим  **JSON Server**  с базой данных **_db.json_**

```console
$ json-server  --watch  <путь к файлу>/db.json
```
Можно использовать сокращение:
```console
$ json-server  <путь к файлу>/db.json  -w
```
Поскольку мы установили  json-server  глобально, <br/>
корневой папкой сайта будет папка <br/>
для установки глобальных пакетов по умолчанию ( **~** )<br/>
Указывая  <путь к файлу>, нужно задавать его относительно этой папки<br/>
> `В данном случае файл `**`users.json`**<br/>
> `находится в папке `**`z:/home/test`**<br/>
> `поэтому нужно указать полный путь к файлу:`
```console
json-server  z:/home/test/users.json –w
```

### :construction: endpoints

Сервер сгенерировал нам **_endpoints_**:
```
http://localhost:3000/users
http://localhost:3000/posts
http://localhost:3000/comments
```
( ссылки на ресурсы **_users_**, **_posts_**, **_comments_**, описанные нами в базе данных **users.json** )

Теперь, пока сервер запущен ( т.е. пока вы не воспользуетесь `Ctrl + C` в консоли _Bush_ ), можно записывать и вытягивать данные из базы данных, пользуясь указанными **endpoints**<br/>
( при этом в консоли  Bush  логируются все запросы )

### fetch

Теперь проверим, как работают наши запросы, из консоли браузера

###### :coffee: :one: GET
```javascript
fetch ( 'http://localhost:3000/comments' )
    .then ( response => response.json ()
        .then ( json => console.log ( json ) )
    )
```
###### :coffee: :two: GET

Теперь получим данные из базы данных в переменные  **_users_**,  **_posts_** и  **_comments_**, используя асинхронную функцию  **getAllData**

Наберем следущий код в консоли браузера:
```javascript
function getData ( ref ) {
    return fetch ( 'http://localhost:3000/' + ref )
        .then ( response => response.json ()
            .then ( json => console.log ( json ) )
        )
}
async function getAllData () {
    var users = await getData ( "users" )
        .then ( response => response )
    var posts = await getData ( "posts" )
        .then ( response => response )
     var comments = await getData ( "comments" )
        .then ( response => response )
    console.log ( users, posts, comments )
}

getAllData ()
```
###### :coffee: :three: POST

Добавим новый комментарий:
```javascript
fetch ( 'http://localhost:3000/comments', {
    method: 'POST',
    body: JSON.stringify ({
        "postId": 1,
      	"userID": 1,
      	"body": "Good for you!"
    }),
    headers: {
        "Content-type": "application/json"
    }
})
    .then ( response => {
        console.log ( 'response: ', response )
})
```
Обратите внимание, что поле **id** добавляемой записи вычисляется на стороне сервера<br/>
Вам не нужно устанавливать его значение<br/>
( но вы можете это делать, если будете отслеживать существующие значения, потому что в противном случае при попытке записи дублирующихся значений **id** будет сгенерировано исключение )

Вытащим добавленный коммент в консоли:
```javascript
fetch ( 'http://localhost:3000/comments?postId=1&id=4' )
    .then ( response => response.json () )
        .then ( json => console.log ( json ) )
```

###### :coffee: :four: PUT
Изменим содержание первого поста :
```javascript
fetch ( 'http://localhost:3000/posts/1', {
    method: 'PUT',
    body: JSON.stringify ({
        userID: 2,
      	title: "My first post here",
      	body: "It's really wonder!"
    }),
    headers: {
        "Content-type": "application/json"
    }
})
   .then ( response => {
       console.log ( 'response: ', response )
})
```
###### :coffee: :five: DELETE

Удалим первый комментарий

В консоли браузера наберем код:
```javascript
fetch ( 'http://localhost:3000/comments/1', {
    method: 'DELETE',
    headers: {
        "Content-type": "application/json"
    }
})
   .then ( response => {
       console.log ( 'response: ', response )
})
```
***
### XMLHttpRequest
```javascript
function workWithData ( method, url, data ) {
    let request = new XMLHttpRequest ()
    request.onreadystatechange = function ( event ) {
        if ( this.readyState === 4 ) 
            if ( this.status === 200 || this.status === 201 )
                console.log ( this.responseText )
        request.open ( method, url )
        request.setRequestHeader ( 
            'Content-type', 'application/json; charset=utf-8' 
        )
        request.send ( data )
}
```
###### GET
```javascript
workWithData (
    'GET',
    'http://localhost:3000/posts'
)
```
###### POST
```javascript
workWithData (
    'POST', 
    'http://localhost:3000/posts',
    JSON.stringify ( {
        userId: 2,
        title: 'XMLHttpRequest',
        body: 'Method POST'
    } )
)
```
###### DELETE
```javascript
workWithData (
    'DELETE',
    'http://localhost:3000/posts/7'
)
```
###### PUT
```javascript
workWithData (
    'PUT', 
    'http://localhost:3000/posts/3', 
    JSON.stringify ( { 
        userId: 2,
        title: "*Бетономешалка",
        body: "Это жесть. Собираюсь купить. Лучше, чем АК!"
    } )
)
```