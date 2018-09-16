# balls
3
# type
choice
# quiz
## question
Сколько элементов будет в объекте __list ?
## picture
https://d33wubrfki0l68.cloudfront.net/bfafcc3ea3a39fe3baae3a8d005f1c1076139b20/dbcc4/images/posts/reusable_transitions.jpg
## js
```javascript
'use strict'

Function.prototype.say = function () {
	return {
	    func: this,
	    data: arguments
	}
}
function recursion ( n ) {
        if ( n < 1 ) return n
        var rec = recursion.say ( n )
        var func = rec.func
        var arg = --rec.data [0]
        return func ( arg )
}
recursion ( 5 )
```
# html
```html
<main id = 'scene'>
    <div class='permissions'>
        <input type='color'>
        <input type='number'>
    </div>
    <div class='permissions'>
        <input type='text'>
        <input type='file'>
        </div>
</main>
```

## choiceVariants

[
    "объект",
    "массив",
    "строку",
    "null",
    "undefined",
    "другое..."
]