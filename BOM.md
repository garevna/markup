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
:white_check_mark: Свойство **`history.state`** ( строка ) содержит адрес текущей страницы

:white_check_mark: Свойство **`history.length`** ( целое число ) содержит число переходов в истории текущей страницы ( `на единицу больше, чем максимально возможное значение для метода go()` )

:white_check_mark: С помощью методов **`history.back()`** и **`history.forward()`** можно управлять переходами назад / вперед по истории

:white_check_mark: С помощью метода **`go()`** ( `если аргумент метода - целое число` ) можно перейти на заданное число страниц вперед ( положительное значение аргумента ) или назад ( отрицательное значение аргумента )

```javascript
window.history.go(-2)
```
>>`В HTML5 были введены методы history.pushState () и history.replaceState (), которые позволяют добавлять и изменять записи истории`
>>[:link: MDN](https://developer.mozilla.org/ru/docs/Web/API/History_API)

Обратите внимание, что свойство **`history.__proto__`** является ссылкой на **`History()`**, а свойство **`history.__proto__.__proto__`** является ссылкой на  **`Object`**

### **`location`**

К свойствам объекта **`location`** относятся:

:white_check_mark: hash
:white_check_mark: host
:white_check_mark: hostname
:white_check_mark: href
:white_check_mark: origin
:white_check_mark: pathname
:white_check_mark: port
:white_check_mark: protocol
:white_check_mark: search

Посмотрим на 
```console
▼ __proto__: Location
    ► constructor: ƒ Location()
      Symbol(Symbol.toStringTag): "Location"
    ► __proto__: Object
```

