|[:rewind:](Fake-chat)|
|-|

```javascript
document.body.style = `
    font-family: monospace, Arial;
    font-size: 14px;
`

let lastUpdate

let getData = function ( ref ) {
    return fetch ( 'http://localhost:3000/' + ref )
        .then ( response => response.json () )
}
let appElem = ( tagName, container ) => 
    ( container ? container : document.body )
        .appendChild ( document.createElement ( tagName ) )

let chat
let posts
let users

let currentUser

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
let updateChat = async function () {
    
    let updated = await getData ( "lastUpdate" )

    if ( lastUpdate &&
         updated.data === lastUpdate.data && 
         updated.time === lastUpdate.time )
        return

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

    lastUpdate = {
        data: updated.data,
        time: updated.time
    }

    chat.scrollTop = chat.scrollHeight
}

let initChat = async function () {
    chat.innerHTML = ""
    posts.forEach ( post => {
        let user = users.filter ( x => x.id === post.userId )[0]
        chat.appendChild (
            ( function () {
                let cont = appElem ( 'div' )
                let ava = appElem ( 'img', cont )
                ava.src = user.photoURL
                ava.width = "40"
                ava.title = ` ${user.name} ${user.lastName}`
                appElem ( 'span', cont ).innerHTML = ` <small> ${post.date} ${post.time}</small>`
                appElem ( 'p', cont ).innerText = post.body
                return cont
            }) ( user )
        )
    })
}

buildChat ()
updateChat ()
setTimeout ( function () {
    chat.scrollTop = chat.scrollHeight
}, 200 )

let interval = setInterval ( function () {
    updateChat ()
}, 500 )

chatInput.onchange = function ( event ) {
    let postTime = new Date().toLocaleString ().split ( ', ' )
    fetch ( 'http://localhost:3000/lastUpdate', {
        method: 'POST',
        body: JSON.stringify ({
            data: postTime [0],
            time: postTime [1]
        }),
        headers: {
            "Content-type": "application/json"
        }
    })
    fetch ( 'http://localhost:3000/posts', {
        method: 'POST',
        body: JSON.stringify ({
            date: postTime [0],
            time: postTime [1],
            userId: currentUser.id,
            body: event.target.value
        }),
        headers: {
            "Content-type": "application/json"
        }
    })
}
```

|[:rewind:](Fake-chat)|
|-|