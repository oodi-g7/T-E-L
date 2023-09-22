# ep8. [Javascript] Ajax Map 넘기기
```javascript
let obj = {};
obj['num'] = num;
obj['id'] = id;
obj['status'] = status;

$.ajax({
    url : '/url',
    type : 'POST',
    data : JSON.stringify(obj),
    contentType : 'application/json;charset=UTF-8',
    dataType : 'text',
    success : function(data){
        console.log(data);
    },
    error : function(err){
        console.log(err);
    }
})
```
- 우선 `let obj = {};` 선언해주고 여기다가 `obj['key'] = value`와 같이 key, value값을 할당한다.
- 이를 ajax를 이용해서 보낼 때는 `JSON.stringify()`를 이용해서 JSON문자열로 변환하여 전달한다. 이때 contentType은 `application/json;charset=UTF-8`이다.

```java
@PostMapping("/url")
public @ResponseBody void test(@RequestBody Map<String, Object> map){
    System.out.println(map.get("num")); // num
    System.out.println(map.get("id")); // id
    System.out.println(map.get("status")); // status
}
```
- 컨트롤러에서 해당 요청을 받을 때는 `@RequestBody Map<String, Object> map`으로 받으며, `map.get("key")`를 이용해서 value값을 가져온다.