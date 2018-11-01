<table>
    <tr>
        <td width="200">
            <img src="https://github.com/garevna/js-course/blob/master/pictures/douglas-crockford.jpg" width="200"/>
        </td>
        <td>
            <p>«<em>Я думаю, что ООП без классов — это подарок человечеству от JavaScript</em>»</p>
            <p><b><a href="http://www.crockford.com/" target="_blank">Дуглас Крокфорд</a></b></p>
        </td>
    </tr>
</table>

## :mortar_board: Фабричные методы

ООП без классов, базирующееся на фабричных методах — 

это новая парадигма программирования, 

позволяющая создавать защищённые и гибкие объекты

    ⛔️ Классы не дают возможности "спрятать" данные внутри экземпляра
    ⛔️ Классы не обеспечивают безопасность 
    ⛔️ Классы не гарантируют нас от потери контекста

***
## :mortar_board: ООП-объекты и структуры данных

| `Роберт Мартин, «Чистый код»:` |
|-:|
| _`Объекты предоставляют поведение и скрывают данные`<br/>`Структуры данных предоставляют данные,`<br/>`но не обладают сколько-нибудь значительным поведением`_ |

#### :coffee: :one:
В этом примере с помощью замыкания создается объект,<br/>
данные которого скрыты от непосредственного доступа<br/>
и доступны только через интерфейс,<br/>
представленный методом **_getVar_**

```javascript
let google = ( function ( params, pin ) {
    return {
        getVar ( varName, pincode ) {
            return pin === pincode ? 
                   params [ varName ] :
                   'No access'
        }
    }
} )( {
    name: "Google",
    token: "A7fgh14-771pd-ufr147"
}, '789541' )

console.log ( google.getVar ( "token" ) )            // No access
console.log ( google.getVar ( "name", "789541" ) )   // Google
```
###### Выведем объект google в консоль:
```javascript
console.log ( google )
```
###### Результат:
```console
▼ User {name: "Google", getVar: ƒ}
  ► getVar: ƒ getVar( varName, pincode )
    name: "Google"
  ► __proto__: Object
```
***
#### :coffee: :two:
В этом примере мы делаем то же самое,<br/>
но используя расширение класса **User**<br/>
Конструктор класса создает публичное свойство **_name_**<br/>
Фабричный метод класса **_updateUser_**<br/>
позволяет расширить функционал класса,<br/>
создать скрытые данные, доступные через интерфейс<br/>
( метод **_getVar_** )
```javascript
class User {
    constructor ( name ) {
        this.name = name || 'unknown'
    }
}
User.updateUser = function ( user, params, pin ) {
    return Object.assign ( user, {
        getVar ( varName, pincode ) {
            return pin === pincode ? 
                   params [ varName ] :
                   'No access'
        }
    })
}

let google = User.updateUser ( new User ( "Google" ), {
        token: "AfG78-1nm*15ph",
        cash: 25000
}, "789451" )

google.getVar( "token", "789451" )  // "AfG78-1nm*15ph"
google.getVar( "cash", "789451" )   // 25000
```
###### Выведем объект google в консоль:
```javascript
console.log ( google )
```
###### Результат:
```console
▼ User {name: "Google", getVar: ƒ}
  ► getVar: ƒ getVar( varName, pincode )
    name: "Google"
  ▼ __proto__:
      ▼ constructor: class User
          ► updateUser: ƒ ( user, params, pin )
            arguments: (...)
            caller: (...)
            length: 1
            name: "User"
            prototype: {constructor: ƒ}
          ► __proto__: ƒ ()
      ► __proto__: Object
```
***
## :mortar_board: Полиморфизм
Фабричные методы дают возможность расширять функциональность конструктора,<br/>
обеспечивая его полиморфизм

В следующем примере конструктор  **User**  имеет фабричный метод   **_createNewUser_**,<br/>
позволяющий создавать экземпляры класса с различным набором свойств и методов

экземпляры   **visitor**  и   **currentUser**,  созданные конструктором  **User**,<br/>
имеют различные свойства и методы

:coffee: :three:
```javascript
function User () {
    this.talk = function ( key ) {
        document.write ( `<p>${key}: <b>${this [ key ]}</b></p>` )
    }
}

User.createNewUser = function( params ) {
    var user = new this
    for ( var key in params ) 
        user [ key ] = params [ key ]
    return user
}

var visitor = User.createNewUser( {
    name: 'migrant',
    timeVisit: new Date ().toLocaleString()
})
visitor.talk ( 'name' )
visitor.talk ( 'timeVisit' )

var currentUser = User.createNewUser ({
    name: prompt( 'What is your name?' ),
    age: prompt( 'How old are you?' ),
    id: Math.round ( Math.random () * 100000000 ),
    posts: {},
    registered: new Date ().toLocaleString().split( ', ' ),
    write: function ( text ) {
        this.posts = Object.assign ( this.posts, {
            [ new Date ().toLocaleString() ] : text
        } )  
    }
})
currentUser.talk ( 'name' )
currentUser.talk ( 'registered' )
currentUser.write ( `I'm here since ${new Date ().toLocaleString()}` )
```
###### visitor
```console
▼ User {talk: ƒ, name: "migrant", timeVisit: "01.11.2018, 13:40:41"}
    name: "migrant"
  ► talk: ƒ ( key )
    timeVisit: "01.11.2018, 13:40:41"
  ► __proto__: Object
```
###### currentUser
```console
▼ User {talk: ƒ, name: "Nick", age: "25", id: 80661698, posts: {…}, …}
    age: "25"
    id: 80661698
    name: "Nick"
  ▼ posts:
        01.11.2018, 13:40:51: "I'm here since 01.11.2018, 13:40:51"
      ► __proto__: Object
  ► registered: (2) ["01.11.2018", "13:40:51"]
  ► talk: ƒ ( key )
  ► write: ƒ ( text )
  ► __proto__: Object
```
```javascript
console.dir ( currentUser.__proto__.constructor )
```
###### currentUser.__proto__.constructor
```console
▼ ƒ User()
    createNewUser: ƒ ( params )
    arguments: null
    caller: null
    length: 0
    name: "User"
    prototype: {constructor: ƒ}
  ► __proto__: ƒ ()
```
Получили _перечислимый_ статический метод **_createNewUser_** конструктора

Сделаем то же самое с помощью класса
```javascript
class User {
    constructor () {
        this.talk = function ( key ) {
            document.write ( `<p>${key}: <b>${this [ key ]}</b></p>` )
        }
    }
    static createNewUser ( params ) {
        var user = new this
        for ( var key in params ) 
            user [ key ] = params [ key ]
        return user
    }
}
```
В этом случае статический метод класса **_createNewUser_**<br/>
будет неперечислимым,<br/>
а в остальном все будет аналогично варианту с конструктором<br/>
<code>Так что "под капотом" работает все то же прототипное наследование,<br/>
только с косметическими "добавками"</code>