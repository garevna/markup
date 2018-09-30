# :mortar_board: Объект **`document`**

Объект **`document`** 

## Свойства

<code>
<b>✅ childNodes</b>

Объект <b><em>[NodeList](#nodeType)</em></b>
<pre>
&lt;body>
  &lt;div class="container" 
          title="Контейнер">
     &lt;a class="paragraph" 
           href="https://translate.google.com/" 
           title="Перевод">Translator
     &lt;/a>
     &lt;img src="http://www.abc.net.au/news/image/9154542-1x1-940x940.jpg" 
             width="200" id="picture" class="galleryPicture">
  &lt;/div>
  &lt;h1 class="header">Hello!</h1>
  &lt;p class="paragraph">You study JS</p>
&lt;/body>

&lt;script>
   <b>document.body.childNodes</b>
   // вернет  NodeList(3) [ div.container, h1.header, p.paragraph ]
   <b>document.querySelector ( '[ title ]' ).childNodes</b>
   // вернет  NodeList(2) [ a.paragraph, img#picture.galleryPicture ]
&lt;/script>
</pre>
[🔗 w3schools](https://www.w3schools.com/jsref/prop_node_childnodes.asp)
</code>
:coffee: 1

<code>
<b>✅ children</b>

Объект <b><em>HTMLCollection</em></b>
</code>
<code>
<b>✅ lastModified</b>

    Строка ( 09/30/2018 11:00:15 )
</code>

## Методы

<a name="nodeType"></a>
### 🎓 Типы узлов дерева DOM

DOM представляет собой граф ( дерево ), вершины которого ( узлы, или **_nodes_** ) могут быть html-элементами, комментариями, обычным текстом...

Получить все дочерние узлы элемента DOM можно с помощью свойства  **`childNodes`**  этого элемента

:coffee: 

```javascript
document.body.childNodes
document.querySelector ( "main" ).childNodes
```
Каждый узел ( объект )  имеет свойство  **_nodeType_**:

| Код | Тип узла | Пример |
|-|-|-|
| `1` | `ELEMENT_NODE` | `<div>` |
| `2` | `ATTRIBUTE_NODE` | `href = "https://translate.google.com/"` |
| `3` | `TEXT_NODE` | `document.body.appendChild ( new Text( "Hello" ) )` |
| `4` | `CDATA_SECTION_NODE` | |
| `5` | `ENTITY_REFERENCE_NODE` | |
| `6` | `ENTITY_NODE` | |
| `7` | `PROCESSING_INSTRUCTION_NODE` | |
| `8` | `COMMENT_NODE` | `<!-- ... -->` |
| `9` | `DOCUMENT_NODE` | `<html>...</html>` |
| `10` | `DOCUMENT_TYPE_NODE` | `<!DOCTYPE>` |
| `11` | `DOCUMENT_FRAGMENT_NODE` | |
| `12` | `NOTATION_NODE` | |

:coffee: 1
```javascript
document.body.appendChild ( new Text( "Hello" ) )
document.body.childNodes
```
```console
▼ NodeList [text]
      0: text
      length: 1
    ► __proto__: NodeList
```
______________________________
https://www.w3schools.com/xml/dom_nodetype.asp