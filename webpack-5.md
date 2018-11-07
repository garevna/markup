### :briefcase: Упражнение 5

    ✅ webpack.config.js
    ✅ style-loader
    ✅ css-loader

#### css-модули

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

#### :wrench: Сборка

А теперь запустим сборку проекта

:no_entry_sign: Вебпак выдаст нам ошибку: 

он умеет собирать модули js, а вот для загрузки файлов других форматов нужны специальные загрузчики

![](https://lh6.googleusercontent.com/9iIWxB9HHuCzZ4ZFlhrUW_GrG3cCX-Y3560mRCPTICdKPAUGNmWgDpwKFuld9rV8dFnVgHIn7Yv0PophBSGy0AqRouju3FG2Jwc6M2ZVNiWRMvpS0sUX7h08HXTsFs_Pzvtjv73t1aqnex8)

### :clipboard: webpack.config.js

Создадим файл  **webpack.config.js**  в корневой папке нашего приложения

Это скрипт, который создаст объект конфигурации `webpack`

Основные свойства объекта конфигурации:

###### :ballot_box_with_check: entry - точка входа
> ###### с этого файла начинается построение графа зависимостей
###### :ballot_box_with_check: output - файл сборки ( результат )
###### :ballot_box_with_check: module - это свойство описывает модули сборки
> ###### по умолчанию модулями являются js-файлы
> ###### для того, чтобы не js-файлы ( например, css или html ) 
> ###### подключались в сборку как модули, нужны специальные загрузчики
> ###### Объект `module` имеет свойство _`rules`_, 
> ###### которое также является объектом и содержит два свойства:
>> ###### ✅ rules
>>>> ###### ✅ test
>>>> ###### ✅ use
>> ###### В свойстве  _`rules.test`_  описывается тип файлов, 
>> ###### которые могут быть загружены как модули ( `regular expression` )
>> ###### В свойстве  _`rules.use`_  указывается загрузчик для файлов данного типа
###### :ballot_box_with_check:plugins - плагины

![](https://lh6.googleusercontent.com/LrTASIeOuHlf0WgAZ6hjzzePQ9ib4NLHzddAUco_ufKMrdtR6yhZ1LAAyAymQPUcYaESRPWU7gOovrdR2zKf1XCt6FR3mkUBXUL2XomNqYIUw7bct0o6BTHQUpY3TT92S6KKA9O5heABRLQ)