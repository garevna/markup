### :briefcase: Упражнение 1

📦 ( zero-config )

Работаем в созданной ранее папке  _test_  `( вы можете назвать свою папку иначе )`

Создаем файлы и папки:

###### :pencil: index.html

```html
<!DOCTYPE html>
<html lang="ru">
    <head>
        <meta charset="UTF-8">
        <title>webpack-sample</title>
    </head>
    <body>
        <div class = "sampleClass"></div>
        <script src = "./dist/main.js"></script>
    </body>
</html>
```
###### :open_file_folder: src

Cоздайте папку  **src**  и поместите туда файл  :pencil: **_index.js_**

###### :pencil: index.js

```javascript
var promise = new Promise ( function ( resolve, reject ) {
    document.write ( 'Wait, pease...<br>' )
    setTimeout ( () => resolve ( "OK, you are here ?" ), 2000 )
})

promise.then ( response => document.write ( response ) )
```
#### webpack

<img src="https://github.com/garevna/js-course/blob/master/images/git-bush-ico.png?raw=true" width="22"/> а теперь выполните в консоли `Git Bush` команду

    webpack

webpack был вызван нами без каких-либо параметров и опций

В консоли видно предупреждение, что опция  **`mode`** отсутствует,<br/>
поэтому использовано значение по умолчанию - **_`production`_**

![](http://icecream.me/uploads/676b38d4712353e1e73a346dd7b55477.png)

Обратите внимание, что в папке проекта появилась новая папка  :open_file_folder: **dist**,

а в этой папке - минифицированный файл  :pencil: **_main.js_**

![](https://lh6.googleusercontent.com/0pagIMHm51JuHbTPqLkRnHIEBD3WxdGhsLjsbb7h0faFhCO7cSVQc2gPhsLvisAFmqwymX0xhX2N4qYMH61DP8L7Aq-VesPwpso5WkBWpmT9WyDw9MU1QG1O7Glri7wN-sGxODtftnmxsOs)

Как видите, мы обошлись без файла конфигурации,<br/>
поскольку  Webpack 4  позволяет это<br/>
при использовании дефолтных имен файлов и папок:

:warning: Исходный файл должен находиться в папке :open_file_folder: **src** и называться :pencil: **_index.js_**

:warning: Результат сборки будет помещен в папку :open_file_folder: **dist** под именем  :pencil: **_main.js_**

Теперь откройте файл  **_index.html_**  в браузере