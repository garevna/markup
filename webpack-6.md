## :briefcase: Упражнение 6

###### ✅ file-loader
***
###### [:link: file-loader](https://www.npmjs.com/package/file-loader)
###### [:link: loaders](https://webpack.js.org/loaders/)
***
### :open_file_folder: images

Создадим папку  :open_file_folder: images в корневой папке нашего проекта<br/>
и поместим туда несколько файлов изображений:

![](https://lh5.googleusercontent.com/dqODscqbar15EGD-mAhay0YwoS0VzKDKpmUKb3_oYfzyLD-I2JbMNGM_6gBhpWsrr5H9_hLWhIDpwsN_w1UMvE38-ccafSB_FiUrrZ_17b-BiM7cItjm2Ku1WFEix9oWFIXUQ8aiI7mmTDM)

### :open_file_folder: js

Добавим  в файл   :pencil: **`script.js`** <br/>
код, который будет добавлять на страницу два элемента  `span`<br/>
с классами  **_git-bush_**   и  **_git_**

Далее внесем соответствующие изменения в файл<br/>
:pencil: **`main.css`**  ( :open_file_folder `css` )

( добавим соответствующие классы )

### :pencil: script.js
```javascript
import promise from './promise.js'
import css from '../css/main.css'

promise.then ( response =>
    document.querySelector ( '.sampleClass' )
        .innerText += response )

document.body.appendChild (
    document.createElement ( 'span' )
).className = 'git-bush'

document.body.appendChild (
    document.createElement ( 'span' )
).className = 'git'
```

### :pencil: main.css

```css
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
}
.sampleClass {
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

### :wrench: file-loader

Установим загрузчик **file-loader**<br/>
и внесем необходимые изменения в файл конфигурации <br/>
:pencil: `webpack.config.js`

    npm install --save-dev file-loader

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
                test: /\.(png|svg|jp?g|gif)$/,
                use: [
                    {
                        loader: 'file-loader',
                        options: {
                            name: 'images/[name].[ext]'
                        }
                    }
                  ]
            },
            {
                test: /\.css$/,
                exclude: /node_modules/,
                use: [
                    'style-loader',
                    'css-loader'
                ]
            },

        ]
    }
}
```

### 🔨 Сборка

Обратите внимание, что после сборки приложения<br/>
все файлы изображений, ссылки на которые были в файле :pencil: **_`main.css`_**,<br/>
оказались в папке :open_file_folder: **`images`**,<br/>
которая была создана в папке :open_file_folder: **`build`**

![](https://lh6.googleusercontent.com/FLcLBZEePLxKPVswXVtkXHofTK2I1wShlFTaWFenTxPXaZRzf1yPSyX8S8mF_sonwERGkos305ZJssSk6Yz04nwPhwK8BVz2jg87eOicg479pjgNiVesfU2x4UH8mOaWJshcN-pZLewfgLI)