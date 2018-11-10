## :mortar_board: customElements.whenDefined

###### Возвращает промис
###### Промис будет разрешен тогда, когда элемент, имя которого передано аргументом, будет определен с помощью метода `customElements.define`

```javascript
customElements.whenDefined( 'circle-element' )
    .then( () => {
        for ( var x of [ "blue", "red", "green", "yellow" ] ) {
            let elem = document.body.appendChild (
                document.createElement ( 'circle-element' )
            )
            elem.backColor = x
            elem.size = 50
            elem.dispatchEvent ( new Event ( "start" ) )
        }
    })

class CircleElement extends HTMLElement {
    constructor() {
        super()
        this.shadow = this.attachShadow ( { mode: 'open' } )
        this.shadow.appendChild (
            document.createElement ( "div" )
        )
        this.addEventListener ( "start", this.setStyle )
    }
    setStyle () {
        this.shadow.appendChild (
            ( () => {
                let style = document.createElement ( "style" )
                style.appendChild (
                    ( () => {
                        let css = document.createTextNode(
                          `
                              div {
                                  width: ${this.size}px;
                                  height: ${this.size}px;
                                  border: inset 1px;
                                  border-radius: 50%;
                                  box-shadow: 3px 3px 5px #00000090;
                                  background-color: ${this.backColor};
                              }
                              div:hover {
                                  box-shadow: inset 3px 3px 5px #00000090;
                              }
                          `
                        )
                        return css
                    })()
                )
                return style
            })()
        )
    }
}

customElements.define ( "circle-element", CircleElement )
```