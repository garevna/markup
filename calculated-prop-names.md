## :mortar_board: Вычисляемые имена свойств
###### ES6

:warning: В качестве имени свойства можно использовать выражение:

:coffee: :one:
```javascript
var bag = {
    [ "prop" + 1 ]: "👜",
    [ "prop" + 2 ]:  '🍄',
    [ "prop" + 3 ]:  "🎓",
}
console.log ( bag.prop1 )  // 👜
console.log ( bag.prop2 )  // 🍄
console.log ( bag.prop3 )  // 🎓
```
:coffee: :two:
```javascript
var prop = "prop"
var id = "____"
var num = [ 1, 2, 3 ]
var bag = {
    [ prop + id + num [ 0 ] ]: "👜",
    [ prop + id + num [ 1 ] ]:  '🍄',
    [ prop + id + num [ 2 ] ]:  "🎓",
}
console.log ( bag.prop____1 )  // 👜
console.log ( bag.prop____2 )  // 🍄
console.log ( bag.prop____3 )  // 🎓
```
:coffee: :three:
```javascript
var prop = [ "smile", "clock", "book" ]
var bag = {
    [ `____${prop [ 0 ]}` ]: "😉",
    [ `____${prop [ 1 ]}` ]:  '⏰',
    [ `____${prop [ 2 ]}` ]:  "📖",
}
console.log ( bag.____smile )  // 😉
console.log ( bag.____clock )  // ⏰
console.log ( bag.____book )   // 📖
```
:coffee: :four:
```javascript
let sample = {}
let props = [ 
    { prop: "mouse", val: "🐭" },
    { prop: "monkey", val: '🐒' },
    { prop: "chicken", val: "🐥" }
]
for ( let x of props ) {
    Object.assign( sample, { [ x.prop ] : x.val } )
}
console.log ( sample.mouse )
console.log ( sample.monkey )
console.log ( sample.chicken )
```