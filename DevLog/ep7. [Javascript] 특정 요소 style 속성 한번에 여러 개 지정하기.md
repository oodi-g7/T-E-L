# ep7. [Javascript] 특정 요소 style 속성 한번에 여러 개 지정하기
```javascript
let target = document.querySelector('요소선택자');
let styles = {
    'width' : '50%',
    'color' : 'yellow',
    'background-color' : 'red'
}

Object.assign(target.style, styles);
```