## :briefcase: Упражнение 8
###### Подключение шрифтов
***
### Google Fonts

Для начала импортируем некоторые шрифты [_**Google**_](fonts.google.com), используя внешний URL

Для этого в наш файл :pencil: **`main.css`** мы добавим строчку
```css
@import url("https://fonts.googleapis.com/css?family=Hanalei+Fill|Roboto");
```
Теперь можно использовать эти шрифты <br/>
( '_Hanalei Fill_', _Roboto_ )<br/>
в своих стилях<br/>
Установим шрифт  '_Hanalei Fill_'   для элемента  `body`<br/>
и шрифт  _Roboto_  для  `.sampleClass`
*** 
###### [Дополнительно](google-fonts-webpack-plugin) ( для самостоятельного изучения ):
***
###### :pencil: main.css
```css
@import url("https://fonts.googleapis.com/css?family=Hanalei+Fill|Roboto:100,300,400");

body {
    position: fixed;
    top: 0;
    left:0;
    bottom:0;
    right:0;
    background-image: url(../images/columns.gif);
    background-repeat: no-repeat;
    background-size: cover;
    background-position: top center;
    font-family: monospace, Arial;
    font-size: 16px;
    color: #abc;
    font-family: 'Hanalei Fill', cursive;
}
.sampleClass {
    font-family: Roboto;
    font-size: 25px;
    font-weight: bold;
}
.git-bush, .git {
    display: inline-block;
    width: 50px;
    height: 50px;
    background-repeat: no-repeat;
    background-size: contain;
    background-position: center center;
}

.git-bush {
    background-image: url(../images/git-bush.png);
}
.git {
    background-image: url(../images/git.png);
}
```
###### 👁‍🗨 Если вебпак находится в режиме отслеживания,<br/>
перезагрузите станицу и вы увидите результат
***
### [Font Awesome](fontawesome.com)
Самый простой способ подключения иконок Font Awesome - импорт в :pencil: **`main.css`**:
```css
@import url("https://use.fontawesome.com/releases/v5.2.0/css/all.css");
```
После этого можно вставить :pencil: **`index.html`**, например, такую строчку:
```html
<i class="fas fa-ambulance"></i>
```
Обновите страницу и вы увидите добавленную иконку