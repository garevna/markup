<a name="top"></a>
# 🎓 Модель наследования JS

| [:arrow_double_down:](#bottom) | <img width="800"/> | [:arrow_heading_down:](#Object) |
|-|-|-|

Модель наследования JS основана на понятии прототипа

**Прототип** - это **объект**

Объект можно создать с помощью конструктора:

:coffee: 1
```javascript
function MasterClass () {
    this.name = "master"
}
function ChildClass () {
    this.__proto__ = new MasterClass ()
    this.name = "child"
}

var obj = new ChildClass ()
```
Экземпляр **obj** в консоли:
```console
▼ ChildClass {name: "child"}
      name: "child"
    ▼ __proto__: MasterClass
         name: "master"
       ▼ __proto__:
            constructor: ƒ MasterClass()
          ► __proto__: Object
```
:coffee: 2
```javascript
var master = { name: "master" }
var child = { name: "child" }
var obj = {}
obj.__proto__ = child
obj.__proto__.__proto__ = master
```
Экземпляр **obj** в консоли:
```console
▼ {}
    ▼ __proto__: 
        name: "child"
      ▼ __proto__: 
          name: "master"
        ► __proto__: Object
```
Добавим метод **_setName_** объекту **`__proto__`**
```javascript
obj.__proto__.setName = function ( val ) {
    this.name = val
}
```
и посмотрим на объект **__child__** ( `который мы не трогали` ) в консоли:
```console
▼ { name: "child", setName: ƒ }
    name: "child"
  ▸ setName: ƒ ( val )
  ▸ __proto__: Object
```
Это свидетельствует о том, что свойство **`__proto__`** экземпляра является **ссылкой** на **объект прототипа**

В обоих примерах легко отслеживается цепочка прототипов

Последним "звеном" в этой цепочке будет **`Object`** - "Адам" всех нативных объектов JS

Заканчивается цепочка прототипов **`null`**

Если возникнет необходимость создать объект без прототипа, можно проделать следующее:
```javascript
var obj = {}
obj.__proto__ = null
```

<a name="Object"></a>
## 🎓 Object

| [:arrow_heading_up:](#enumerable) | <img width="800"/> | [:arrow_heading_down:](#bottom) |
|-|-|-|

Прототипом всех создаваемых нативных объектов является встроенный объект  **Object** ( конструктор )

У конструктора  **Object**  есть свойство  **`prototype`**

Это "генокод" всех создаваемых объектов JS

Он передается им при "рождении"

Все свойства и методы, перечисленные в свойстве **`prototype`** объекта  **Object**, будут доступны в каждом экземпляре создаваемого нативного объекта JS

```javascript
var obj = {}

obj.valueOf ()
obj.toString ()
```
***
| [:arrow_heading_up:](#Object) | <a name="bottom"><img width="800"/></a> | [:arrow_double_up:](#top) |
|-|-|-|

[:briefcase: Упражнения](https://docs.google.com/forms/d/e/1FAIpQLSf-i0cr7AEXzSJrggqS1AgZz-OBW5ES-l_ntO1R4Q7XZqZaEw/viewform)
***
[:link: MDN](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects)
[:link: MDN](https://developer.mozilla.org/ru/docs/Web/JavaScript/Introduction_to_Object-Oriented_JavaScript)