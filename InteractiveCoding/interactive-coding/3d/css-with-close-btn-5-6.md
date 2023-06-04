# css 작업 with 'close btn' #5 #6

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

index.html

```markup
      <div class="page-face">
        3B
        <button class="close-btn">✗ Close</button>
      </div>
```

close 버튼은 3B에 붙붙어야함.



main.css

```css
.close-btn {
	/* display: none; */
	position: absolute;
	top: -2rem;
	right: 10px;
	font-size: 1.2rem;
	color: #fff;
	text-shadow: rgba(0, 0, 0, 0.3) 0 1px 0;
	backface-visibility: hidden;
}

.leaflet-opened .close-btn {
	display: inline-block;
}
```

top에 -를 주면서 강제로 끌어올림.



main.js의 closeLeaflet 함수

```javascript

function closeLeaflet() {
    pageCount = 0;
    
    document.body.classList.remove('leaflet-opened');
    pageElems[2].classList.remove('page-flipped');
    setTimeout(() => {
        pageElems[0].classList.remove('page-flipped');
    }, 500);
}
```



main.js 전역 변수 선언

```javascript
let pageCount = 0;
const pageElems = document.querySelectorAll('.page');
```



main.js의 addEventListener에&#x20;

* pageCount 시스템 추가
* 클릭시 타겟이  closeBtnElem dom  여부 확인

```javascript
leaflet.addEventListener('click', e => {
  let pageElem = getTarget(e.target, 'page');

  // console.log(pageElem)
  if (pageElem) {
    pageElem.classList.add('page-flipped')
    pageCount++;

    if (pageCount == 2) {
      document.body.classList.add('leaflet-opened');
    }
  }
  
  let closeBtnElem = getTarget(e.target, 'close-btn');
    if (closeBtnElem) {
    	closeLeaflet();
    	//zoomOut();
    }
})
```



```javascript


```

