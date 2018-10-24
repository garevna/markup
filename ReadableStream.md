## :mortar_board: ReadableStream

###### Конструктор

Создает экземпляры класса **ReadableStream**

```console
▼ ƒ ReadableStream
    arguments: (...)
    caller: (...)
    length: 0
    name: "ReadableStream"
  ▼ prototype:
      ► cancel: ƒ cancel()
      ► constructor: ƒ ReadableStream()
      ► getReader: ƒ getReader()
        locked: (...)
      ► pipeThrough: ƒ pipeThrough()
      ► pipeTo: ƒ pipeTo()
      ► tee: ƒ tee()
      ► get locked: ƒ locked()
      ► __proto__: Object
  ► __proto__: ƒ ()
```
###### Получение объекта класса `ReadableStream`
```javascript
fetch ( 'http://ptsv2.com/t/garevna/d/980001/json')
   .then ( response => console.log ( response.body ) )
```
###### Результат
```console
▼ ReadableStream {}
    locked: (...)
  ▼ __proto__:
      ► cancel: ƒ cancel()
      ► constructor: ƒ ReadableStream()
      ► getReader: ƒ getReader()
        locked: (...)
      ► pipeThrough: ƒ pipeThrough()
      ► pipeTo: ƒ pipeTo()
      ► tee: ƒ tee()
      ► get locked: ƒ locked()
      ► __proto__: Object
```
### :mortar_board: getReader

```javascript
fetch ( 'http://ptsv2.com/t/garevna/d/980001/json')
   .then ( response => 
      console.log ( response.body.getReader() ) 
   )
```
###### Результат
```console
▼ ReadableStreamDefaultReader {}
    closed: (...)
  ▼ __proto__:
      ► cancel: ƒ cancel()
        closed: (...)
      ► constructor: ƒ ReadableStreamDefaultReader()
      ► read: ƒ read()
      ► releaseLock: ƒ releaseLock()
      ► get closed: ƒ closed()
      ► __proto__: Object
```
> `Метод read() возвращает промис`

### :mortar_board: read()

```javascript
fetch ( 'http://ptsv2.com/t/garevna/d/980001/json')
   .then ( response => 
      response.body.getReader().read()
         .then ( response => console.log ( response ) )
   )
```
###### Результат
```console
▼ {value: Uint8Array(1401), done: false}
    done: false
  ► value: Uint8Array(1401) [123, 34, 84, 105, 109, 101, 115, 116, 97, 109, 112, 34, 58, 34, 50, 48, 49, 56, 45, 49, 48, 45, 50, 52, 84, 48, 55, 58, 48, 52, 58, 49, 56, 46, 48, 57, 51, 49, 90, 34, 44, 34, 77, 101, 116, 104, 111, 100, 34, 58, 34, 80, 79, 83, 84, 34, 44, 34, 82, 101, 109, 111, 116, 101, 65, 100, 100, 114, 34, 58, 34, 49, 56, 53, 46, 51, 56, 46, 50, 49, 55, 46, 54, 57, 34, 44, 34, 73, 68, 34, 58, 57, 56, 48, 48, 48, 49, 44, 34, 72, …]
  ► __proto__: Object
```

### :mortar_board: ArrayBuffer
```javascript
fetch ( 'http://ptsv2.com/t/garevna/d/980001/json')
   .then ( response => 
      response.body.getReader().read()
         .then ( response => {
            var buffer = new ArrayBuffer ( response.value.length )
            response.value.map ( ( value, i ) => { buffer[i] = value } )
            console.log ( buffer ) 
         })
   )
```
###### Результат
```console
ArrayBuffer(1401) {0: 123, 1: 34, 2: 84, 3: 105, 4: 109, 5: 101, 6: 115, 7: 116, 8: 97, 9: 109, 10: 112, 11: 34, 12: 58, 13: 34, 14: 50, 15: 48, 16: 49, 17: 56, 18: 45, 19: 49, 20: 48, 21: 45, 22: 50, 23: 52, 24: 84, 25: 48, 26: 55, 27: 58, 28: 48, 29: 52, 30: 58, 31: 49, 32: 56, 33: 46, 34: 48, 35: 57, 36: 51, 37: 49, 38: 90, 39: 34, 40: 44, 41: 34, 42: 77, 43: 101, 44: 116, 45: 104, 46: 111, 47: 100, 48: 34, 49: 58, 50: 34, 51: 80, 52: 79, 53: 83, 54: 84, 55: 34, 56: 44, 57: 34, 58: 82, 59: 101, 60: 109, 61: 111, 62: 116, 63: 101, 64: 65, 65: 100, 66: 100, 67: 114, 68: 34, 69: 58, 70: 34, 71: 49, 72: 56, 73: 53, 74: 46, 75: 51, 76: 56, 77: 46, 78: 50, 79: 49, 80: 55, 81: 46, 82: 54, 83: 57, 84: 34, 85: 44, 86: 34, 87: 73, 88: 68, 89: 34, 90: 58, 91: 57, 92: 56, 93: 48, 94: 48, 95: 48, 96: 49, 97: 44, 98: 34, 99: 72, …}
```
### :mortar_board: Blob
```javascript
fetch ( 'http://ptsv2.com/t/garevna/d/980001/json')
   .then ( response => {
      console.log ( response.body )
      response.body.getReader().read()
         .then ( response => {
            var buffer = new ArrayBuffer ( response.value.length )
            response.value.forEach ( 
                ( val, index ) => {
                    buffer [ index ] = val
                } 
            )
            var blob = new Blob ( [ buffer ] )
            console.log ( blob )
         })
   })
```
###### Результат
```console
▼ Blob(1401) {size: 1401, type: ""}
    size: 1401
    type: ""
    __proto__: Blob
```