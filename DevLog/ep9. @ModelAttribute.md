# ep9. [Spring] @ModelAttribute 이용 다중 조건 검색 구현하기
```java
@Getter
@Setter
@ToString
public class VideoSetInfo{
    private int preset_id;
    private String user_name;
    private String start_dt;
    private String video_set_name;
    private int flag;
}
```
```HTML
<form action="/workList/form?search">
	<div class="search-start-date">
	  <p>날짜</p>
    <input class="start-dt" type="date" name="start_dt">
  </div>
	<div class="search-preset">
		<p>적용한 프리셋</p>
		<select class="preset" name="preset_id">
			<option value="-1">전체</option>
			<option th:each="preset : ${preset_list}" th:value="${preset.preset_id}" 
			th:text="${preset.preset_name}"></option>
		</select>
	</div>
	<div class="search-set-name">
		<p>영상세트명</p>
		<input class="set-name" type="text" name="video_set_name" placeholder="영상세트명 입력">
	</div>
	<div class="search-set-status">
		<p>상태</p>
		<select class="status" name="flag">
			<option value="-1">전체</option>
			<option value="0">대기</option>
			<option value="1">AI분석중</option>
			<option value="2">재수행중</option>
			<option value="3">완료</option>
			<option value="4">오류</option>
		</select>
	</div>
	<div class="search-username">
		<p>사용자</p>
		<input class="username" type="text" name="user_name" placeholder="사용자명 입력">
	</div>
	<div class="search-button">
		<button onclick="workList.clickSearchButton()">검색</button>
	</div>
</form>
```
- 검색 Form을 만들어 /workList/form?search 와 같이 Mapping 주소를 적은 후 Get방식으로 파라미터를 보낸다.
    - Form 안에 Input 또는 Select의 name속성은 앞서 만들어둔 VideoSetInfo 의 필드와 동일하게 작성해준다.
```java
@Controller
@RequestMapping("/workList")
public class WorkListController {

    @GetMapping("/form")
    public String worklist_form(@AuthenticationPrincipal PrincipalDetails userDetails,
                                @ModelAttribute("search") VideoSetInfo search, Model model) {
            
            System.out.println(search);

            return null;
    }
}
```
- 이제 컨트롤러에서 @ModelAttribute 를 이용하여 아까 get방식으로 보내준 파라미터인 search를 VideoSetInfo 타입으로 받는다. 이를 출력해 보면 다음과 같다.
    > VideoSetInfo(preset_id=-1, video_set_name=, flag=-1, user_name=, start_dt=) 
- 검색 조건을 입력하여 요청을 보내도 아래와 같이 정상적으로 출력된다.
    > VideoSetInfo(preset_id=72, video_set_name=0913테스트, flag=1, user_name=김은지, start_dt=2023-09-18)