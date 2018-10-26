# :mortar_board: REST
###### Representational State Transfer
***
Обычно URL указывает на _ресурс_

В архитектуре **REST** :warning: URL указывает на _операцию с ресурсом_

Для каждой операции с ресурсом ( GET, POST, PUT, DELETE ) устанавливается <b>endpoint</b> ( URL )<br/>

###### :coffee: POST
```console
http://ptsv2.com/t/garevna/post
```
###### :coffee: GET в формате JSON-строки
```console
http://ptsv2.com/t/garevna/d/940001/json
```
###### :coffee: GET в текстовом формате
```console
http://ptsv2.com/t/garevna/d/940001/text
```

###### Автор концепции
| Roy Thomas Fielding |  |
|:-:|:-:|
| <img width="200" src="https://pbs.twimg.com/profile_images/2195030209/roy_fielding_sq.jpg"/> | `DOCTOR OF PHILOSOPHY`<br/>_`in Information and Computer Science`_<br/>[DISSERTATION](https://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm) |

## :mortar_board: HATEOAS

✅ **_[Hypermedia](#hypermedia) As The Engine Of Application State_** ( **HATEOAS** ) — <br/>
это специфическое ограничение архитектуры **REST**, отличающее его от других сетевых архитектур

**_HATEOAS_** разделяет клиента и сервер, позволяя функционалу сервера развиваться независимо

**REST API**  предоставляет URL-ссылки на _**разрешенные операции с ресурсами**_

**`endpoint`** — точка взаимодействия клиента с API

> `URL-ссылки не содержат никакой информации о том, где размещен ресурс`<br/>
> `клиент не знает ( и не должен знать ) URL ресурса`<br/>
> `если ресурс будет перемещен на другой сервер, клиент этого не узнает`<br/>
> `он будет по-прежнему работать с ресурсом по тем же URL-ссылкам`<br/>
> `каждая такая ссылка является `**`endpoint`**<br/>
> **`endpoint`**` - это некая операция с ресурсом`<br/>

###### ⚠️ Итак, API предоставляет клиенту  endpoints  для доступа к ресурсу
###### ⚠️ API решает, какие операции может выполнять клиент с ресурсом
###### ⚠️ Для каждой операции есть свой endpoint

***
<a name="hypermedia"></a>
**`Hypermedia`**` — это способ структурирования информации и доступа к её элементам с помощью `_`гиперсвязей`_