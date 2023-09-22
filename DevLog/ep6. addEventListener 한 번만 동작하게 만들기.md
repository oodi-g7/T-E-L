# ep6. [Javascript] addEventListener 한 번만 동작하게 만들기

```javascript
1. addEventListener(type, listener);
2. addEventListener(type, listener, option);
```

- 이벤트 등록 시 보통 1번을 많이 쓰는데, 2번처럼 옵션을 줄 수 있다.

```javascript
document.querySelector('엘리먼트ID 또는 클래스명')
        .addEventListener('click', (e)=>{
            // 함수내용
        }, {once : true});
```
- {once : true} 이렇게 옵션을 지정하면 Listener가 발동된 후 제거된다.
- 해당 Listener가 여러번 호출될 경우, 이벤트가 여러번 적용되어 한번 클릭했는데 여러번 클릭된 것처럼 동작하는 경우가 생길 수 있다. 그럴 때 해당 옵션을 부여하면 removeEventListener를 해줄 필요 없이 깔끔하게 코드 작성이 가능하다.