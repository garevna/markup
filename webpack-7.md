## :briefcase: Упражнение 7
###### Именованный экспорт

### Веб-компонент

Создадим новый файл :pencil: **_`PictureSlider.js`_**<br/>
в папке :open_file_folder: **`js`**

Обратите внимание, что в этом файле мы используем именованный экспорт <br/>
( два объекта экспортируются из одного файла )

✅ export class PictureSlider<br/>
✅ export const Slide

В файле  :pencil: **_`PictureSlider.js`_**<br/>
определим веб-компонент,<br/>
который получает массив входных параметров<br/>
( ссылки на изображения )<br/>
через атрибут src

###### :pencil: PictureSlider.js
```javascript
export class PictureSlider extends HTMLElement {
    constructor () {
        super()
        this.pictures = []
        this.container = this.createElem ( 'figure' )
        this.getData ()
        this.currentIndex = 0
        this.currentSlide = 0
        let shadow = this.attachShadow ( { mode: 'open' } )
        shadow.appendChild ( this.container )
        let style = document.createElement ( 'style' )
        style.textContent = `
            figure {
                position: fixed;
                top: 10%;
                left: -10%;
                bottom: 10%;
                right: -10%;
                overflow: hidden;
            }
            button {
                position: absolute;
                top: 50%;
                font-size: 30px;
                z-index: 100;
                background: transparent;
                border: 0;
                color: white;
                text-shadow: 3px 3px 5px #00000090;
                outline: none;
                font-family: monospace;
            }
            button:hover {
                font-size: 32px;
                text-shadow: 2px 2px 4px #000000b0;
            }
            #left { left: 10%; }
            #right { right: 10%; }
            div {
                position: absolute;
                top: 10%;
                bottom: 10%;
                background-repeat: no-repeat;
                background-size: contain;
                background-position: center center;
                transition: all 0.8s;
            }
        `
        shadow.appendChild ( style )

        this.btnLeft = this.createElem ( 'button', this.container )
        this.btnLeft.id = 'left'
        this.btnLeft.onclick = () => this.changePicture ( "left" )
        this.btnRight = this.createElem ( 'button', this.container )
        this.btnRight.id = 'right'
        this.btnRight.onclick = () => this.changePicture ( "right" )
        this.btnLeft.innerHTML = '<'
        this.btnRight.innerHTML = '>'
    }
    createElem ( tagName, container ) {
        return  ( !container ? document.body : container )
                .appendChild (
                    document.createElement ( tagName )
                )
    }

    async getData () {
        let __self = this
        this.pictures = await  new Promise ( function ( resolve ) {
            setTimeout ( () => resolve ( __self.src ), 100 )
        } )
        this.slides = []
        this.slides [ 0 ] = new Slide (
            this.pictures [ 0 ],
            this.container
        )
        this.slides [ 0 ].mcFromTo ( 100, 10 )
        this.slides [ 1 ] = new Slide (
            this.pictures [ 1 ],
            this.container
        )
        this.slides [ 1 ].init ( 100 )
    }
    changePicture ( direction ) {
        let to = direction === 'left' ? 100 : -100
        let nextSlide = this.currentSlide === 0 ? 1 : 0
        let nextIndex = this.getNextIndex ( direction )
        this.slides [ nextSlide ].setPicture ( this.pictures [ nextIndex ] )
        this.slides [ nextSlide ].init ( -to )
        this.slides [ this.currentSlide ].mcFromTo ( 10, to, 0 )
        this.slides [ nextSlide ].mcFromTo ( -to, 10, 1 )
        setTimeout ( function () {
            this.currentSlide = nextSlide
            this.currentIndex = nextIndex
        }.bind(this), 1000 )
    }

    getNextIndex ( dir ) {
        return dir === 'left' ?
            ( this.currentIndex === 0 ?
                this.pictures.length - 1 : this.currentIndex - 1 ) :
                    ( this.currentIndex === this.pictures.length - 1 ?
                        0 : this.currentIndex + 1 )
    }
}

export const Slide = function ( imageURL, container ) {
    this.imageURL = imageURL
    let elem = container.appendChild (
        document.createElement ( 'div' )
    )
    elem.style = `
        background-image: url(${imageURL});
    `
    this.init = function ( x ) {
        elem.style.left = x + '%'
        elem.style.width = container.style.width * 0.8
    }
    this.setPicture = pictureURL => {
        elem.style.backgroundImage = `url(${pictureURL})`
    }
    this.mcFromTo = function ( from, to, finalOpacity ) {
        elem.style.transition = 'none'
        elem.style.left = from + '%'
        elem.style.opacity = 1 - finalOpacity
        elem.style.width = container.offsetWidth * 0.8 + 'px'
        setTimeout ( function () {
            elem.style.transition = 'all 0.8s'
            elem.style.left = to + '%'
            elem.style.opacity = finalOpacity
        }, 50 )
    }
}
```
###### :pencil: script.js
```javascript
'use strict'

import promise from './promise.js'
import { Slide, PictureSlider } from './PictureSlider.js';
import css from '../css/main.css';

promise.then ( response =>
    document.querySelector ( '.sampleClass' )
        .innerText += response 
)

document.body.appendChild (
    document.createElement ( 'span' )
).className = 'git-bush'

document.body.appendChild (
    document.createElement ( 'span' )
).className = 'git'

customElements.define (
    'picture-slider',
    PictureSlider
)
var slider = document.body.appendChild (
    document.createElement ( 'picture-slider' )
)

slider.src = [
    "https://www.sunhome.ru/i/cards/113/otkritki-valentine-s-day-kartinki.orig.jpg",
    "http://img.over-blog-kiwi.com/0/98/03/83/20160127/ob_d8f5c9_12163786387fxcdr3.jpg",
    "http://www.tematy.info/library/c/cute-cartoon-flowers-with-faces/cute-cartoon-flowers-with-faces-19.jpg",
    "http://papers.co/wallpaper/papers.co-nx17-sunset-river-lake-beautiful-nature-28-wallpaper.jpg"
]
```
