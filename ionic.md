## ionic + angular 'memo'

---
  - ionic CLI 생성시 4개 파일 자동생성 (ionic start)
  1. **.html**
  2. **.scss**
  3. **.module.ts** > route 연결
  4. **.ts** > script 파일<br>
  (app.component >> index)

---
- angular = html >> .ts로 접근가능(변수, 컴포넌트(private x) > default = public)
- F2 로 잡아서 수정할 때 >> .ts만 변경됨/ html > 수동으로 직접 수정해야함!
- [()] 양방향 바인딩
  - [https://angular.kr/guide/two-way-binding](https://angular.kr/guide/two-way-binding)
  - 말그대로 in & out을 서로에게 주는 형식

---
- ngOnInit () {}
  - 보통 export class 뒤에 implements OnInit 과 함께 쓰인다(셋뚜)
  - ngOnInit () {} 안에 쓰여지는 함수 순서대로 호출된다

---
### 이슈완료 🔚

1. git branch (feature/ 'branch이름') 확인
    
    
    ![image](https://user-images.githubusercontent.com/79742210/140269174-8574505e-621d-40e2-9d8f-f07aff013363.png)

2. git commit -am "fix: ~이슈 요약~ "
    

    ![image](https://user-images.githubusercontent.com/79742210/140269249-abcb9c10-5685-485e-8ad8-969e7fcf95e6.png)

    
3. git push
    
    ![image](https://user-images.githubusercontent.com/79742210/140269285-5774123c-ff30-480a-81c8-454489e2b57b.png)
    
    - git push 할때, use git push —블라블라 나오면, 그대로 복붙에서 push~

---
1. switch - case (return or break이 있어야 빠져나갈 수 있음) + translate.instant 로 활용 (언어파일에서 {}로 가져오기)
2. export enum ScState {} (booking-model.ts) → ScState.Adding 요런형식으로 가져오기위해 모아둔거( . 으로 경로 접근)
    
    ![image](https://user-images.githubusercontent.com/79742210/140269426-7a34862a-8688-4288-b0af-dd847838e675.png)

    
3. class 에서 화살표함수 보기 (class안에서 this.를 접근하기 위해서 쓰임)/ class 일반함수에서는 this.로 접근불가 > 일반적으로 쓰는 {}형식으로 쓰기 위해서!
4. *ngIf 문 > 부모(html)에서 if 조건이 true → 자식(ts)로 접근해서 그려줌/ []로 자식에게 넘겨줄 값을 지정한다 → 지정한 값에 대한 함수 등 실행되서 html에 보여줌
5. for (const t of tl.trainerList) {} / t는 tl.trainerList 안에있는 모든 []를 돌려준다! (뱅뱅도는 for문)

---
### event.stopPropagation()
- propagaion = 전파, 확산이라는 뜻을 가짐
1. 버튼을 클릭했을 때, 웹 페이지 내부에서는 버튼을 감싸고 있는 부모 태그들 또한 클릭에 대한 이벤트에 반응함 >  `Bubble Up` 
2. ex) ul > li > a : button(click) 이러한 형태로 있을때, click 이벤트가 발생하면 a → li → ul 로 올라가면서 이벤트가 실행된다
    1. 만약 ul에도 click 이벤트가 있다면 >> a 태그를 클릭하는 순간 ul 의 click 이벤트가 실행
3. 👉🏻 이러한 상황에서 ul(부모태그)로의 이벤트 전파를 막기위해서 `**stopPropagation**` 사용

---
### event.preventDefault()
```
<a href='#' class='expand'></a>
```
- a 태그를 클릭했을 때 2가지 이벤트가 실행됨
    1. click 이벤트 실행 > a 태그는 click 이벤트도 가지고 있기 때문!
    2. 웹 브라우저에게 href 에 표시된 곳으로 이동하도록 실행

- 위 a 태그는 내부적으로 href='#' 라는 속성을 가지고 있음, href는 웹 브라우저에게 a 태그 클릭시 이동하여야할 페이지를 그려줌
    - href = '#' 로 속성값을 설정한 이유 = a 태그에는 click 이벤트가 있으니, click 이벤트만 실행하고 웹브라우저는 이동하지 말아라~ 라고 말해주는거!
    - 하지만, 다른 페이지로 이동하지 않을뿐! 스크롤이 있는 곳에서는 페이지 상단으로 이동하도록 만들어져서 클릭할 때 마다 페이지가 위로 올라감 ㅜㅜ

- 👉🏻  이러한 상황에서 a 태그처럼 클릭이벤트 외 별도의 브라우저 행동을 막히위해서 `**preventDefault**` 사용
---
### keyboardEvent
- keydown = 키가 눌린 경우 트리거 발생
- keypress = 웹 표준에서 제거/ 캐릭터 값을 생성하는 경우 트리거 발생(printable key에 대해서만 트리거 발생)
- keyup = 키가 떼질 때(release) 트리거 발생

→ keydown/ keyup = 눌린 키에 대해 알려주며, down > press > up 순서대로 발생함
