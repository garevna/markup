## :briefcase: Упражнение 5

    ✅ webpack.config.js
    ✅ style-loader
    ✅ css-loader
***
### css-модули

Создадим в папке нашего проекта папку :open_file_folder: css

Поместим в нее файл  :pencil: main.css

#### :pencil: main.css
```css
body {
        background-color: #000;
        font-family: monospace, Arial;
        font-size: 16px;
        color: #9ab;
}
```
![](https://lh5.googleusercontent.com/oSo7naNlVfS1BFfQ3ybg_bemnZmkDEZKTVrbvxsMjvbCye6wc4DQOO68r1PKQv-MfTtBsdgxep9v98fC6QHu6sGAGx_offjUo-FyNI-3-8RD1iQGMpTAchMMuKpHoZmY2bH5YyIse38gFvk)

#### :pencil: script.js
Добавим в файл  `script.js`  импорт созданного нами файла стилей:
```javascript
import css from '../css/main.css'
```
![](https://lh6.googleusercontent.com/E60i49827-g4mBJR28bIYMYU2D0NGi7FlnCkYNgkdNVSX4QYCmlAH4nLLJWltIqIns3ymwNfgvOKLJFeFC0ydtEkf6w3SDUgXzUZ5btCJXix4jJZqt4xbLrsRHTsVTDLB7NKtp4lUEktyBs)
***
### :wrench: Сборка

А теперь запустим сборку проекта

:no_entry_sign: Вебпак выдаст нам ошибку: 

он умеет собирать модули js, а вот для загрузки файлов других форматов нужны специальные загрузчики

![](https://lh6.googleusercontent.com/9iIWxB9HHuCzZ4ZFlhrUW_GrG3cCX-Y3560mRCPTICdKPAUGNmWgDpwKFuld9rV8dFnVgHIn7Yv0PophBSGy0AqRouju3FG2Jwc6M2ZVNiWRMvpS0sUX7h08HXTsFs_Pzvtjv73t1aqnex8)
***
### :clipboard: webpack.config.js

Создадим файл  **webpack.config.js**  в корневой папке нашего приложения

Это скрипт, который создаст объект конфигурации `webpack`

#### Основные свойства объекта конфигурации:
<table>
   <tr>
      <td>:ballot_box_with_check:</td>
      <td><code><b>entry</b></code></td>
      <td><code>точка входа</code></td>
      <td><code>с этого файла начинается построение графа зависимостей</code></td>
   </tr>
   <tr>
      <td>:ballot_box_with_check:</td>
      <td><code><b>output</b></code></td>
      <td><code>файл сборки</code></td>
      <td><code>результат работы webpack</code></td>
   </tr>
   <tr>
      <td>:ballot_box_with_check:</td>
      <td><code><b>module</b></code></td>
      <td><code>описание модулей</code></td>
      <td>
         <code>по умолчанию модули - это <b>js</b>-файлы</code><br/>
         <code>для подключения в качестве модулей файлов с другим расширением ( например, <b>.css</b> или <b>.html</b> )
         нужны специальные программы-загрузчики</code><br/>
         <code>Проги-загрузчики "обертывают" содержимое нужного файла в скрипт, чтобы превратить их в "нормальные" модули</code><br/>
         <code>Объект <b>module</b> имеет свойство <b><em>rules</em></b> ( объект с двумя свойствами ):</code><br/>
         &nbsp;&nbsp;<code><b>module</b></code><br/>
         &nbsp;&nbsp;<code>&nbsp;&nbsp;↪ <b><em>rules</em></b></code><br/>
         &nbsp;&nbsp;<code>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↪ test &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; тип файла модулей (/\.css$/)</code><br/>
         &nbsp;&nbsp;<code>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↪ use &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; загрузчик для файлов этого типа</code><br/>
      </td>
   </tr>
   <tr>
      <td>:ballot_box_with_check:</td>
      <td><code><b>plugins</b></code></td>
      <td><code>плагины</code></td>
      <td>
      </td>
   </tr>
</table>

### :pushpin: path
Для разрешения конфликтов маршрутов ( путей ) к различным файлам сборки 

первым делом в файле кофигурации webpack ( webpack.config.js ) 

подключайте встроенный Node.js-модуль `path`:
```javascript
const path = require ( 'path' )
```
Теперь можно использовать глобальную переменную  **_`__dirname`_** для получения абсолютного пути к файлу с помощью метода  **`path.resolve`**

Например, путь к папке  **_build_**, находящейся в корневой папке приложения:
```javascript
path.resolve ( __dirname, "build" )
```

### Подключение css-модулей
Для подключения css-файла нужно указать  в файле :pencil: `webpack.config.js`

( в объекте конфигурации, в свойстве **`module`** )

правило, по которому будут обрабатываться файлы с расширением  **`css`**

Для этого в свойстве  **`module.rules`** мы определим значение свойства **_`test`_**

с помощью регулярного выражения:  **`/\.css$/`** `( любые файлы с расширением css )`

а свойство **`module.rules.use`** сделаем массивом, в котором передадим ссылки на загрузчиков:
```javascript
[  'style-loader',  'css-loader'  ]
```
###### :pencil: webpack.config.js
```javascript
const path = require ( 'path' )

module.exports = {
   entry: { main: './js/script.js' },
   output: {
      path: path.resolve ( __dirname, 'build' ),
      filename: 'index.js'
   },
   module: {
      rules: [
         {
            test: /\.css$/,
            use: [
               'style-loader',
               'css-loader'
            ]
         }
      ]
   }
}
```
***
[:link: Regular Expressions](https://developer.mozilla.org/ru/docs/Web/JavaScript/Guide/Regular_Expressions)
***
### <img src="https://lh5.googleusercontent.com/jtBBT0GcTBpcVz_jTSw_mjrkA50bE7le_iDcw_QUqhKl70Fkgw3p_iWWLZwPl5FtiLXxXttIX3uXgGGYbYyoZAsz2aK2lhhu86x8M17xn_zXkdOYjXozof1rZ7UdzquMsqQTCkkBCydA5Qc" width="120"/> `module.exports`
Для того, чтобы вы понимали, почему в файле  :pencil: _webpack.config.js_ используется  **`module.exports`**, и как это работает, нужно понимать следующее:

В  **Node.js**:

✋  **`module`** - это объект JS,  у которого есть свойство  ☝ **_`exports`_**

Если в  файле :pencil: _sourse.js_ определено свойство **`module.exports`**, в любом другом файле  ( например,  :pencil: _sample.js_ ) можно вызвать функцию  🛒 **_require_** и передать ей в качестве аргумента имя файла ( "sourse.js" )

Результатом работы функции  🛒 **_require_** будет объект, ссылку на который мы поместили в **`module.exports`** в файле :pencil: _sample.js_

:coffee: :one:

###### :pencil: script.js
```javascript
module.exports = {
    hello: function () {
        console.log ( 'Привет, будущие девелоперы!' )
    },
    message: function ( mess ) { console.log ( mess ) }
}
```
###### :pencil: start.js  :
```javascript
let lib = require ( './script.js' )
lib.hello ()
lib.message ( "Вы еще не знакомы с Node.js ?" )
```
<img src="https://gitforwindows.org/img/gwindows_logo.png" width="30"/> Запустим теперь команду:
```
npm run start
```
###### <img src="https://gitforwindows.org/img/gwindows_logo.png" width="22"/> Результат:
```
> npm-test@1.0.0 start Z:\home\npm-test
> node start.js

Привет, будущие девелоперы!
Вы еще не знакомы с Node.js ?
```

### :wrench: Установка загрузчиков
<img src="https://gitforwindows.org/img/gwindows_logo.png" width="22"/>

```
npm install css-loader style-loader --save-dev
```

![](https://lh5.googleusercontent.com/ctLeetPIQ0Bsol7YcR3GC0Qixw4p7xoKnaCivTnevYg86sTwezG9f5vYHAXHGd8Af-M8dVzryfOpC682knlYug_aVafWxnpUxUnpcxmuX1hctX_A1Djj4hNguJYB_ktbmR2SSpTwMW08jAQ)

После установки загрузчиков они окажутся в папке :open_file_folder: **`node_modules`** проекта

:warning: Обратите внимание, что в файле **`package.json`** появилось свойство **_`devDependencies`_**, в котором перечислены установленные нами загрузчики с указанием версии пакета

###### package.json

![](http://icecream.me/uploads/1ecae9d3709876ce3b8cfee212dc4059.png)

### :wrench: Сборка
###### <img src="https://gitforwindows.org/img/gwindows_logo.png" width="30"/>
![](https://lh6.googleusercontent.com/LrTASIeOuHlf0WgAZ6hjzzePQ9ib4NLHzddAUco_ufKMrdtR6yhZ1LAAyAymQPUcYaESRPWU7gOovrdR2zKf1XCt6FR3mkUBXUL2XomNqYIUw7bct0o6BTHQUpY3TT92S6KKA9O5heABRLQ)

👁‍🗨 Вебпак находится в режиме отслеживания наших файлов

Теперь перезагрузите страницу, в которой открыт файл **`index.html`**, и вы увидите, что созданный нами файл стилей подключен

Мы можем внести изменения в любой из наших файлов, и эти изменения будут автоматически отображены в файле сборки

Давайте, например, добавим в файл **_main.css_**:
```css
img { margin: 40px; border: dotted 2px yellow; }
```
перезагрузите страницу, и вы увидите изменения 