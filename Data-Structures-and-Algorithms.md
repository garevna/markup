Структуры данных - это способы организации и хранения данных
Алгоритм — последовательность действий ( операций )

Структуры данных и алгоритмы тесно связаны
В зависимости от выбранной структуры данных применяются различные алгоритмы доступа к данным

Алгоритмы характеризуются производительностью
Под производительностью алгоритма понимается:
     - число операций алгоритма ( от чего зависит время выполнения )
     - объем необходимой памяти

Основные структуры данных:

* Связный список
* Динамический массив
* Стеки и очереди
* Графы
* Двоичное дерево поиска

### Бинарное дерево

У каждого дерева есть корень ( root ) и узлы ( node )
Двоичное дерево: 
     - каждый узел имеет не более двух дочерних узлов
     - левый дочерний узел имеет значение, меньше чем значение родительского узла
     - правый дочерний узел имеет значение, больше или равное значению родительского узла

### Коллекции
###### Конструктор
```javascript
var Collection = function ( name, createItem ) {
        this.items = []
        this.name = name || "collection"
        this.itemsCounter = ( function () {
                var counter = 0
                return function ( operationType ) {
                        return Math.abs ( operationType ) !== 1 ? counter : counter += operationType 
                } 
        })()
        this.createItem = typeof createItem === "function" ? createItem : null
}
Collection.prototype.removeItem = function ( itemNum ) {
        if ( itemNum > this.itemsCounter () ) return false
        this.items = this.items.filter ( x => {
                if ( x.index > itemNum ) {
                        --x.index
                }
                return x.index !== itemNum
        })
}
Collection.prototype.addItem = function ( item ) {
        item.index = this.itemsCounter ( 1 )
        this.items.push ( this.createItem ? this.createItem ( item ) : item )
}
```
###### Использование

var tags = new Collection ( "elements", function ( params ) {
        var elem = document.createElement ( params.tagName || "div" )
        var parentElement = params.parent || document.body
        parentElement.appendChild ( elem )
        if ( params.id ) elem.id = params.id
        if ( params.className ) elem.id = params.className
        elem.innerHTML = params.innerHTML || ""
        
        if ( params.styles && typeof params.styles === "object" ) {
                for ( var x in params.styles ) {
                        console.log ( x )
                        elem.style [ x ] = params.styles [x]
                }
        }
        return elem
} )