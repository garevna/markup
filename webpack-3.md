## :briefcase: Упражнение 3

### :pencil: package.json

Откройте файл  **_package.json_**  и добавьте в свойство **`scripts`** в настройки запуска webpack :
```javascript
"scripts": {
    "dev": "webpack --mode development",
    "prod": "webpack --mode production"
}
```
<img src="http://icecream.me/uploads/d2f7543e47891188282c5f21075ea5bd.png" width= "550"/>

###### Опция  --mode  позволяет настроить режим сборки

###### :warning: --mode development
    результирующий бандл не будет минимизирован,
    в консоль будут выводится сообщения об ошибках
    используется на этапе отладки
###### :warning: --mode production
    результирующий бандл будет минимизирован,
    это окончательная сборка проекта - production

<img src="https://gitforwindows.org/img/gwindows_logo.png" width="24"/> Теперь запустите команду :

    npm run dev

###### npm run prod
Теперь соберите свое приложение для  production

Обратите внимание, насколько сократился размер результирующего файла  main.js 
