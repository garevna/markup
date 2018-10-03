_( черновик )_
# :mortar_board: Browser Object Model

## Объект window

Посмотрим на свойство **`window.__proto__`** в консоли:

```console
▼ __proto__: Window
      PERSISTENT: 1
      TEMPORARY: 0
    ► constructor: ƒ Window()
      Symbol(Symbol.toStringTag): "Window"
    ▼ __proto__: WindowProperties
        ► constructor: ƒ WindowProperties()
          Symbol(Symbol.toStringTag): "WindowProperties"
        __proto__: EventTarget
            ► addEventListener: ƒ addEventListener()
            ► dispatchEvent: ƒ dispatchEvent()
            ► removeEventListener: ƒ removeEventListener()
            ► constructor: ƒ EventTarget()
              Symbol(Symbol.toStringTag): "EventTarget"
            ► __proto__: Object
```

К числу свойств объекта  **window** относятся следующие объекты:

```
    ✅ console
    ✅ navigator
    ✅ screen
    ✅ location
    ✅ history
    ✅ document
```

У каждого из этих объектов есть свои свойства и методы

Методами объекта  **`console`**  мы уже пользовались

**_viewport_** - часть окна браузера, где отображается веб-страница 
( `без панелей и элементов управления самого браузера` )

### **`history`**
Посмотрим на объект **`history`** в консоли:

```console
▼ history: History
      length: 2
      scrollRestoration: "auto"
      state: null
    ▼__proto__: History
        ► back: ƒ back()
        ► forward: ƒ forward()
        ► go: ƒ go()
          length: (...)
        ► pushState: ƒ pushState()
        ► replaceState: ƒ replaceState()
          scrollRestoration: (...)
          state: (...)
        ► constructor: ƒ History()
          Symbol(Symbol.toStringTag): "History"
        ► get length: ƒ ()
        ► get scrollRestoration: ƒ ()
        ► set scrollRestoration: ƒ ()
        ► get state: ƒ ()
        ► __proto__: Object
```
<code>

✅ Свойство <b>history.state</b> ( строка ) содержит адрес текущей страницы

✅ Свойство <b>history.length</b> ( целое число ) содержит число переходов в истории текущей страницы ( `на единицу больше, чем максимально возможное значение для метода go()` )

✅ С помощью методов <b>history.back()</b> и <b>history.forward()</b> можно управлять переходами назад / вперед по истории

✅ С помощью метода <b>go()</b> ( `если аргумент метода - целое число` ) можно перейти на заданное число страниц вперед ( положительное значение аргумента ) или назад ( отрицательное значение аргумента )
</code>
```javascript
window.history.go(-2)
```
>>`В HTML5 были введены методы history.pushState () и history.replaceState (), которые позволяют добавлять и изменять записи истории`
>>[:link: MDN](https://developer.mozilla.org/ru/docs/Web/API/History_API)

Обратите внимание, что свойство **`history.__proto__`** является ссылкой на **`History()`**, а свойство **`history.__proto__.__proto__`** является ссылкой на  **`Object`**

### **`location`**

К свойствам объекта **`location`** относятся:

    ✅ hash
    ✅ host
    ✅ hostname
    ✅ href
    ✅ origin
    ✅ pathname
    ✅ port
    ✅ protocol
    ✅ search

Посмотрим на 
```console
▼ __proto__: Location
    ► constructor: ƒ Location()
      Symbol(Symbol.toStringTag): "Location"
    ► __proto__: Object
```

### [:briefcase: Упражнения](https://docs.google.com/forms/d/e/1FAIpQLSegoz325rD2axv1Trw3EYZVPFhXbRaEa40WQhSO22EzEEYvZA/viewform) 