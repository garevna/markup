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

<img src="https://lh3.googleusercontent.com/9Kw0fdiVv9zrVzwLuN9mgI_kTysz4yCDr_pz4DixW9p4EHJnAtuiYC2zjZ_Zua4hZNB9J_7mwNOsVS8BnCpsJs7MmSkxSALp431a-mnwUIog458xNgcAxmUALDz9ddZsAEqqIWRyt9V37Vg" width="500"/>

###### npm run prod
Теперь соберите свое приложение для  production

Обратите внимание, насколько сократился размер результирующего файла  main.js 

<img src="https://lh3.googleusercontent.com/y8ZDRi431GzQ2QJjKd5u8rm9NehAdfgq48K6jtahgt1NPWZ6YY_pp_Ut_HBcJ5alQ0Zp6kHNCBqnxTM9iq2cUncPrNVvKwA9i5NsBce78yhOfFWmOxrF9KmBeahFEbSum1Q2g-B07GLC3qo" width="500"/>
