| [:rewind:](Class#mortar_board-extends) |
|-|

:coffee: :nine:
```javascript
const Canvas = class {
    constructor () {
        this.canvas = document.createElement ( 'canvas' )
        document.body.appendChild ( this.canvas )
        this.canvas.height = "400"
        this.area = this.canvas.getContext ( "2d" )
    }
    drawLine ( points ) {
        this.area.beginPath()
        this.area.moveTo( points[0].x, points[0].y )
        this.area.lineTo( points[1].x, points[1].y )
        this.area.stroke()
    }
}

class ExtendedCanvas extends Canvas {
    drawCircle ( center, radius ) {
        this.area.beginPath()
        this.area.arc( center.x, center.y, radius, 0, 2 * Math.PI )
        this.area.stroke()
    }
}

let newCanvas = new ExtendedCanvas ()
newCanvas.drawCircle ( { x: 100, y: 100 }, 100 )
newCanvas.drawLine (  [ { x: 20, y: 20 }, { x: 300, y: 400 } ] )
```

| [:rewind:](Class#mortar_board-extends) |
|-|