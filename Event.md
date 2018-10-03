# :mortar_board: Events

R

```console
▼ ƒ EventTarget()
    arguments: null
    caller: null
    length: 0
    name: "EventTarget"
    ▼ prototype: EventTarget
        ► addEventListener: ƒ addEventListener()
        ► dispatchEvent: ƒ dispatchEvent()
        ► removeEventListener: ƒ removeEventListener()
        ► constructor: ƒ EventTarget()
          Symbol(Symbol.toStringTag): "EventTarget"
        ► __proto__: Object
    ► __proto__: ƒ ()
```

:coffee: 1
```javascript
function addElement ( tagName, container ) {
    var _container = 
        container && container.nodeType === 1 ? 
                    container : document.body
    return _container.appendChild (
         document.createElement ( tagName )
    )
}

var obj = addElement ( "h1" )

obj.innerText = "Hi"

obj.addEventListener ( "listen", listenHandler )

function listenHandler ( event ) {
    this.innerText = event.detail
}

var btn = addElement ( "button" )
btn.innerText = "Change"

btn.onclick = function ( event ) {
    var inp = addElement ( "input" )
    inp.onchange = function ( event ) {
        obj.dispatchEvent ( 
             new CustomEvent ( "listen",
                  { 
                       detail: this.value
                  } 
             ) 
        )
        this.parentNode.removeChild ( this )
    }
}
```