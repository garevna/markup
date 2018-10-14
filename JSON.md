## :mortar_board: JSON
>> Формат хранения объектов JS  в виде текстовой строки удобен с точки зрения обмена данными с сервером и хранения данных сложной структры

>> Он является более компактной альтернативой формату **XML** ( e**X**tensible **M**arkup **L**anguage )


**`JSON`** - это встроенный нативный объект ( не конструктор )

Имеет всего два метода:

###### ✅ **JSON.stringify ()**
###### ✅ **JSON.parse ()**

```console
▼ JSON
    ► parse: ƒ parse()
    ► stringify: ƒ stringify()
      Symbol(Symbol.toStringTag): "JSON"
    ▼ __proto__:
        ► constructor: ƒ Object()
        ► hasOwnProperty: ƒ hasOwnProperty()
        ► isPrototypeOf: ƒ isPrototypeOf()
        ► propertyIsEnumerable: ƒ propertyIsEnumerable()
        ► toLocaleString: ƒ toLocaleString()
        ► toString: ƒ toString()
        ► valueOf: ƒ valueOf()
        ► __defineGetter__: ƒ __defineGetter__()
        ► __defineSetter__: ƒ __defineSetter__()
        ► __lookupGetter__: ƒ __lookupGetter__()
        ► __lookupSetter__: ƒ __lookupSetter__()
        ► get __proto__: ƒ __proto__()
        ► set __proto__: ƒ __proto__()
```

## :mortar_board: `JSON.stringify ()`

* Единственный обязательный аргумент метода - ссылка на объект ( массив )
* Возвращаемое значение -  JSON-строка

:coffee: :one: 
```javascript
var obj = {
   name: "sample",
   type: "figure",
   color: "green",
   size: 200,
   position: [ 250, 250 ]
}

JSON.stringify ( obj )
```

```console
'{"name":"sample","type":"figure","color":"green","size":200,"position":[250,250]}'
```

## :mortar_board: `JSON.parse ()`

* Единственный обязательный аргумент метода - JSON-строка
* Возвращаемое значение - объект JS

###### :warning: В строке  JSON  все строчные значения ( включая имена свойств )  заключаются в `двойные` кавычки
###### :warning: Числовые и логические значения, массивы и объекты в кавычки не заключаются

:coffee: :two: 
```javascript
var x = `{
    "name": "sample",
    "type": "figure",
    "attrs": {
           "color": "green",
           "size": 200,
           "position": [ 250, 250 ]
    }
}`

JSON.parse ( x )
```

```console
▼ {name: "sample", type: "figure", attrs: {…}}
  ▼ attrs:
        color: "green"
      ► position: (2) [250, 250]
        size: 200
      ► __proto__: Object
    name: "sample"
    type: "figure"
  ► __proto__: Object
```

## :mortar_board: Глубокое копирование

Известно, что массивы и объекты передаются по ссылке

Если объект имеет плоскую структуру, то получить точную копию этого объекта можно с помощью метода **`Object.assign ()`**

Однако если свойства объекта являются объектами или массивами, то **`Object.assign ()`** скопирует ссылки на эти вложенные объекты

Если же выполнить сначала **`JSON.stringify ()`**, а затем **`JSON.parse ()`**, то в результате мы получим точную копию объекта, а не ссылку

:coffee: :three:
```javascript
var obj = {
        name: "sample",
        type: "figure",
        color: "green",
        size: 200,
        position: [ 250, 250 ]
}
var sample = JSON.parse ( JSON.stringify ( obj ) )
```
В переменной **sample** теперь находится точная копия объекта **obj**, включая значения элементов массива **position**, а не ссылка на него

Сравним результаты  **`Object.assign ()`** и  **`JSON.stringify ()`** :arrow_right: **`JSON.parse ()`**

```javascript
var test = Object.assign ( {}, obj )
```
Логическое выражение
```javascript
test.position === obj.position
```
возвращает `true`, поскольку значение свойства  **test.position** является ссылкой на объект **obj.position**

А вот логическое выражение
```javascript
sample.position === obj.position
```
вернет  `false`, потому что **sample.position** является другим объектом, ссылка на который не совпадает со ссылкой на объект **obj.position**
