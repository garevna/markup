### :briefcase: Упражнение 4

#### Настройки  webpack
Переименуем  папку :open_file_folder: `src`

Пусть теперь она называется  :open_file_folder: **js**

Переименуем также файл  :pencil: `index.js`

Пусть теперь он называется  :pencil: **script.js**

Теперь изменим настройки запуска webpack в файле  `package.json`:

###### :pencil: package.json
```javascript
"scripts": {
    "dev": "webpack --mode development ./js/script.js --output ./build/index.js --watch",
    "build": "webpack --mode production ./js/script.js --output ./build/index.js --watch"
}
```
<img src="https://lh4.googleusercontent.com/t3HMzsLvURk-jymxhIhITlzHUVfrkuS1UagnldLwLccys2iZH8rBOFWdLf16gh1UqinQ8gjibPgIlqkp5PvYtAaC0hBwA32nscUHScKfZGFdgiWJHwMOyP7NU70qhWGZF87lOjmc7TfY4L8" width="800"/>

###### :pencil: index.html
Не забудьте внести соответствующие изменения в файл :pencil: **_index.html_**

Результирующий бандл будет теперь в папке  :open_file_folder: **build**
и называться он будет  :pencil: index.js

Изменим значение _src_ тега  `script` соответствующим образом:

<img src="https://lh4.googleusercontent.com/mzuMRK4yXEhLJ1AW0sBaSswsz35bNA9srOzeQQx0EjWI2xUK7zzeADS9SdFh7g2heeuuBAQLMQYNI4xvVuiVOak-GOMQ88SpmSYE4ERCcYvRtFxg8prqo1pOyl5vy-mDY__8weNvaQ-wXhw" width="500"/>

### :wrench: Сборка
Теперь запускайте сборку приложения одной из команд:

    npm run dev       

или

    npm run build

( мы заменили _prod_ на **_build_** в  `package.json` )

и открывайте  index.html  в браузере
***
### :wrench: npm run dev

#### 👁‍🗨 --watch
Сейчас   webpack   находится в режиме наблюдения за нашими исходными файлами, <br/>
потому что мы использовали опцию **`--watch`**

Давайте внесем изменения в файл  :pencil: **_script.js_**

###### :pencil: script.js
```javascript
import promise from './promise.js'

promise.then ( response =>
  document.querySelector ( '.sampleClass' ).innerText += response )

document.body.appendChild (
    document.createElement ( 'img' )
).src = "https://sites.google.com/site/eternalfallout/alienhead-detailed.jpg"
```

Перезагрузите страницу в браузере, и вы увидите, что  webpack автоматически собрал заново наше приложение, и внесенные нами изменения уже отображаются на странице 😉

Теперь можно удалить папку :open_file_folder: **_dist_**