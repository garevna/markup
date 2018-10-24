### :clipboard: namedItem

С помощью метода **`namedItem`** можно получить ссылку на именованный элемент из таких HTML-коллекций ( _**`HTMLCollection`**_ ), как:

    ✅ document.forms
    ✅ document.images
    ✅ document.anchors
    ✅ document.all
    ✅ document.scripts
    ✅ document.links
    ✅ document.plugins
```html
<form name="form">
    <a name="ref">🏠</a>
    <img name="picture"/>
</form>
<div id="div"></div>
<script name="script"></script>
```
```javascript
console.log (
    document.forms.namedItem ( "form" ),
    document.anchors.namedItem ( "ref" ),
    document.images.namedItem ( "picture" ),
    document.scripts.namedItem ( "script" ),
    document.all.namedItem ( "div" )
)
```
### HTMLCollections

| Element | id | name |
|-|-|-|
| documenmt.forms | :large_blue_circle: | :large_blue_circle: |
| document.anchors | :large_blue_circle: | :large_blue_circle: |
| document.images | :large_blue_circle: | :large_blue_circle: |
| document.scripts | :large_blue_circle: | :large_blue_circle: |
| document.links | :red_circle: | :red_circle: |

### document.all.namedItem

Используем функцию:

```javascript
function testNamedItem ( tagName ) {
    var elem = document.body.appendChild ( 
        document.createElement ( tagName )
    )
    elem.id = "testId"
    elem.name = "testName"
    console.log ( 'by id:   ', document.all.namedItem ( "testId" ) ? "✅" : "⛔️" )
    console.log ( 'by name: ', document.all.namedItem ( "testName" ) ? "✅" : "⛔️" )
    document.body.removeChild ( elem )
}
```
для получения инфо о том, как работает метод **_namedItem_** для различных элементов DOM

| Element | id | name |
|-|-|-|
| form | :large_blue_circle: | :large_blue_circle: |
| a | :large_blue_circle: | :large_blue_circle: |
| img | :large_blue_circle: | :large_blue_circle: |
| input | :large_blue_circle: | :large_blue_circle: |
| select | :large_blue_circle: | :large_blue_circle: |
| textarea | :large_blue_circle: | :large_blue_circle: |
| script | :large_blue_circle: | :red_circle: |
| link | :large_blue_circle: | :red_circle: |
| div | :large_blue_circle: | :red_circle: |
| ul | :large_blue_circle: | :red_circle: |
| li | :large_blue_circle: | :red_circle: |

###### Самостоятельно проверьте остальные элементы