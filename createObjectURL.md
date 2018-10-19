| [:rewind:](fetch) |
|-|

### :mortar_board: URL.createObjectURL()
статический метод конструктора URL

* Аргумент метода - объект типа **File** или **Blob**
* Метод создает ссылку ( URL ) на локальный объект, переданный аргументом
* * :warning: `Созданная ссылка существует до закрытия окна браузера или перезагрузки страницы`
* Созданный объект URL связан со страницей, где выполняется скрипт
* * :warning: `File API запрещает кросс-доменное использование объекта URL` 
> Этот метод удобен для вывода изображений, полученных методом **`fetch`**  в формате **_`blob`_**

:coffee:

```javascript
fetch ( 'https://avatars2.githubusercontent.com/u/46?v=4' )
    .then ( response => {
        response.blob().then ( response => {
    	    urlObject = URL.createObjectURL( response)
    	    console.log ( urlObject )
        })
    })
```
В консоли мы увидим:
```
blob:null/3163e503-d619-4de0-922a-36990f3fdab7
```
Этот метод можно использовать для вывода на страницу загруженных пользователем изображений

При этом формируется ссылка на локальный файл на компе пользователя, как если бы он был выложен в сети

***

| [:rewind:](fetch) | [:coffee:](https://codepen.io/garevna/pen/odZPbx) |
|-|-|