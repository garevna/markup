| [:rewind:](Class) |
|-|

### :coffee: Пример

В этом примере мы будем работать с  svg-графикой

###### SVG Tutorial:
| [:link: w3schools](https://www.w3schools.com/graphics/svg_intro.asp) | [:link: htmlacademy](https://htmlacademy.ru/blog/127-a-guide-to-svg-on-web) |
|-|-|

#### createElementNS()

☝ Для динамического создания элементов SVG нужно использовать метод **`createElementNS()`**<br/>
с указанием ссылки на пространство имен ( **_NS_** )

Это необходимо для того, чтобы браузер правильно понимал и отображал _svg_-элементы

SVG - это тип XML-разметки, который имеет собственное пространство имен, которое может быть встроено в HTML5

✅ Первым аргументом метода  **`createElementNS()`** идет ссылка на пространство имен<br/>
( `http://www.w3.org/2000/svg` )<br/>
✅ Второй аргумент - имя тега элемента в этом пространстве имен

✋ Если использовать обычный метод  `createElement()`, то браузер будет интерпретировать его в пространстве имен  HTML<br/>
( по умолчанию )

✋ Для корректной работы svg-элементов нужно, чтобы браузер интерпретировал их в пространстве имен SVG

`Например, чтобы корректно создать контейнер для  svg-графики:`
```javascript
document.createElementNS ( "http://www.w3.org/2000/svg", "svg" )
```
###### Проверим в консоли:
```javascript
let x = document.createElement ( "svg" )
x.namespaceURI  // "http://www.w3.org/1999/xhtml"

let x = document.createElementNS ( "http://www.w3.org/2000/svg", "svg" )
x.namespaceURI  // "http://www.w3.org/2000/svg"
```

###### Valid Namespace URIs:
     ✅ HTML - http://www.w3.org/1999/xhtml
     ✅ SVG - http://www.w3.org/2000/svg

#### Базовый класс

Создадим класс  **DrawFigures**, который будет создавать  элемент  svg<br/>
с двумя методами:   **_setSize()_**  и  **_drawFigure()_**

✍ Метод **_setSize()_** будет изменять размеры элемента  svg<br/>
✍ Метод **_drawFigure()_** будет добавлять элементы в контейнер  svg<br/>

    Имя элемента будет передано первым аргументом метода  ( figure )
    возможные значения  "line", "circle", "path", "rect" и т.д.
    Параметры фигуры будут переданы вторым аргументом метода 
    ( params )

✍ Поскольку у каждого элемента  svg  свой набор атрибутов, создаем свойство  **_attrs_** ( объект ), свойства которого будут именами svg-элементов, а значения - массивом атрибутов каждого svg-элемента

При создании svg-элемента его атрибуты будут установлены с помощью метода  **_setAttribute()_**
```javascript
const DrawFigures = class SVG {
    constructor ( w, h ) {
        this.canvas = document.createElementNS ( "http://www.w3.org/2000/svg", "svg" )
        document.body.appendChild ( this.canvas )
        this.setSize ( w, h )
        this.attrs = {
            line: [ "x1", "y1", "x2", "y2" ],
            circle: [ "cx", "cy", "r" ]
        }
    }
    setSize ( w, h ) {
        this.canvas.setAttribute ( "width", w )
        this.canvas.setAttribute ( "height", h )
    }
    drawFigure ( figure, params ) {
        var elem = document.createElementNS ( "http://www.w3.org/2000/svg", figure )
        this.canvas.appendChild ( elem )
        for ( var x of this.attrs [ figure ] ) {
            elem.setAttribute ( x, params [ x ] )
        }
        return elem
    }
}
```
###### Протестировать работу класса можно так:
```javascript
let sample = new DrawFigures( 300, 300 )
sample.drawFigure ( "line", { x1: 10, y1: 20, x2: 250, y2: 250 } )
                        .setAttribute ( "stroke", "red" )
```
> Вызов метода   **_drawFigure()_** создаст элемент &lt;line> и вернет ссылку на него,<br/>
но этот элемент не отобразится на странице, поскольку в массиве  **_attrs.line_**<br/>
нет атрибута "`stroke`", задающего цвет линии

✏️ Чтобы увидеть этот элемент на странице, нам приходится устанавливать значение атрибута `stroke`<br/> 
после вызова метода **_drawFigure()_**:
```javascript
setAttribute ( "stroke", "red" )
```
✏️ Теперь можно рисовать и другие фигуры, и настраивать их атрибуты:
```javascript
var circle = sample.drawFigure ( "circle", { cx: 180, cy: 180, r: 150 } )
circle.setAttribute ( "stroke", "blue" )
circle.setAttribute ( "fill", "transparent" )
sample.setSize ( 400, 400 )
circle.setAttribute ( "stroke-width", 8 )
```
[:coffee: Пример в песочнице](https://garevna.github.io/js-samples/#18)

#### Дочерний класс
Теперь создадим дочерний класс  **ColoredFigures**, <br/>
расширяющий функционал родительского класса  **DrawFigures**<br/>
путем добавления атрибутов линий и заливки фигур <br/>
( "`stroke`", "`style`", "`fill`" )<br/>
и метода удаления элемента  **_erase_**

В конструкторе дочернего класса вызовем метод **`super()`**, <br/>
чтобы был создан контейнер <svg> с нужными размерами, <br/>
и объявим свойство экземпляра  **_figures_**

Метод **`super()`** должен быть вызван первым в конструкторе, <br/>
поскольку до его вызова  значение  `this`  не будет определено <br/>
внутри конструктора 

Кроме того, расширим функционал базового класса  **DrawFigures**,<br/>
добавив атрибуты  "`stroke`",  "`style`"  и  "`fill`"
это мы тоже сделаем в конструкторе класса  **ColoredFigures**

```javascript
class ColoredFigures extends DrawFigures {
    constructor () {
        super ( window.innerWidth - 20, window.innerHeight - 20 )
        this.figures = []
        for ( let x in this.attrs ) {
            this.attrs [x].push ( "stroke", "style", "fill" )
        }
    }
    line ( params, line ) {
        this.draw ( "line", params )
    }
    circle ( params, line, fill ) {
        this.draw ( "circle", params )
    }
    draw ( figure, params ) {
        if ( params.strokeWidth ) {
            Object.assign ( params, { 
                style: `stroke-width: ${ params.strokeWidth }` 
            } )
            delete params.strokeWidth
        }
        var fig = this.drawFigure ( figure, params )
        this.figures.push ( fig )
    }
    erase ( figure ) {
        if ( figure > this.figures.length - 1 || figure < 0 ) return
        var deleted = this.figures [ figure ]
        deleted.parentNode.removeChild ( deleted )
        this.figures.splice ( figure, 1 )
    }
}
```
###### Проверим, как работает расширенный класс  **ColoredFigures**
```javascript
let canvas = new ColoredFigures ( 400, 500 )

canvas.line ( { 
        x1: 10, 
        y1: 250, 
        x2: 250, 
        y2: 50, 
        stroke: "green", 
        strokeWidth: 5 
} )
canvas.circle ( { 
        cx: 150, 
        cy: 150, 
        r: 100, 
        fill: "#ff00ff90", 
        stroke: "#909", strokeWidth: 10 
} )
```
Конечно, мы можем создавать элементы, обращаясь к методу базового класса  **_drawFigure()_**:
```javascript
canvas.drawFigure ( "line", { 
        x1: 200, 
        y1: 150, 
        x2: 50, 
        y2: 100, 
        stroke: "blue", 
        style: "stroke-width: 10" 
} )
```
но тогда созданные svg-элементы не попадут в массив  **_figures_**<br/>
и их нельзя будет удалить с помощью метода  **_erase()_**

Кроме того, вызов метода  **_line()_**  или  **_circle()_**  лаконичнее

    ☝ Обратите внимание, 
    что у класса  ColoredFigures  
    есть свойство  prototype,
    которого нет ( и не может быть ) у экземпляра

    В свойстве  prototype  
    класса  ColoredFigures  
    находятся методы  circle(),
    line(),  draw()  и   erase() 

    ☝ У класса  ColoredFigures  
    есть также свойство  __proto__ 
    это ссылка на родительский класс SVG

    ☝ У родительского класса, 
    как и следовало ожидать, 
    тоже есть свойство prototype,
    и в этом свойстве находятся 
    методы drawFigure() и setSize()

    ☝ Ни у класса ColoredFigures,  
    ни у класса SVG  
    нет свойств attrs, canvas и figures
    Они есть только 
    у экземпляра этого класса

***

| [:rewind:](Class) |
|-|