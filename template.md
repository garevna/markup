# :mortar_board: &lt;template>

    ✅ DocumentFragment
    ✅ content
    ✅ cloneNode ()

Элемент &lt;template> предназначен для хранения шаблона разметки
###### :warning: Он не отображается на странице
###### :warning: Он парсится браузером, поэтому должен содержать только валидный код разметки

:coffee: :one:
Откроем вкладку **Elements** инструментов разработчика и вставим в элемент `body` следующий код разметки:
```html
<body>
    <template id="sample">
        <h3>Template header</h3>
        <p>Template text</p>
    </template>
</body>
```
При этом на странице ничего не появится, а вот во вкладке  **Elements**  мы увидим следующую картинку
```html
▼ <template id="sample">
  ▼ #document-fragment
     <h3>Template header</h3>
     <p>Template text</p>
  </template>
```