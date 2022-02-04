## ionic + angular 'memo'

### angular의 LifeCycle Hook Event

1. **construcotr**
    - angular와 별개로 .ts에서 호출하는 method
    - constructor가 실행된 후 angular LifeCycle 실행
2. **ngOnChange** 
    - 자식 component에서 @Input을 이용하면, 부모 component에서 property를 전달 받을 수 있음
    - 부모 component에서 전달해주는 property가 변경되면 ngOnChange가 재호출!
    - 부모로부터 같은 값을 호출받거나, 전달받은 값이 객체 내의 property만 바뀐경우에는 호출 x
3. **ngOnInit**
    - ngOngChange 이후에 호출, 초기에 한번만 호출됨
    - class가 가지고 있는 property와 @Input으로 내려받은 property가 모두 초기화 된 이후 호출!
    - 화면에 Data 가 표시되기 전 필요한 property등을 초기화 시키는데 사용!
4. **ngDoCheck**
    - component의 상태를 감지함
    - 상태가 변경됨을 감지할 때마다 호출되기 때문에 되도록 사용 x
5. **ngAfterViewInit**
    - component view가 완전히 초기화 되었을 때 실행! (자식 component 포함) 이는 오직 component에만 적용!
    - 자식 component까지 초기화 후 실행되는 특성으로, 부모 component -> 자식 component에 접근하는 @viewchild를 사용할 때 이를 사용
6. **ngOnDestroy**
    - component가 종료되기 전에 subscribed, event등 핸들러를 제거할 때 사용!


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

---
### Directive (in Angular)
- Angualr의 `Directive` = DOM의 모양/ 동작들을 지시하기 위한 명령(DOM을 제어하기 위한 용도)
    - `HTML Element or Element의 attribute` 형태로 사용되게 됨(ngIf 처럼!)
    - 기본적으로는 해당 component를 이용하면 가능함!
    
    → 하지만 여러 view에서 공통적으로 사용하는 Element or Element의 attribute 등을 directive로 지정해두면 component의 복잡도를 낮출 수 있고, 유지보수가 편함
    
    → component도 큰 의미에서 directive라고 해석할 수 있음.

- Directive의 종류
    1. Component Directive : 우리가 알고 있는 Component로 selector에서 directive를 지정해서 사용하게 됨
    2. Attribute Directive : HTML Element의 Attribute로 사용됨 (ex - ngClass 등)
    3. Structural Directive : DOM을 제어하기 위한 directive (ex - ngIf, ngFor, ngSwitch 등)
    4. Custom Directive : 직접 만들어서사용하는 directive
    
    1. `Structural Directive` > ngIf, ngFor 등
        - Angular 는 동일한 Element에 두개 이상의 *ngIf, *ngFor, *ngSwitch 를 사용할 수 없음 !
        
        → 해서 이런걸 해결하기 위해 ng-container를 제공
        
    
    1. `Custom Directive` > 말그대로 custom해서 사용하는 directive
    
    ```tsx
    import {Direcitve, ElementRef } form '@angular/core';
    	// 1) Directive를 사용해서 만들기 때문 2) ElementRef로 내보내주기 때문 -> Directive 와 ElementRef import
    
    @Directive ({ selector: '[focusOnInit]' })
    	// Directive로 만들고 어떤이름으로 쓸지 정해주어야함
    
    export class FocusOnInitDirective extends BaseComponent {
    	pulic constructor(
    		private elementRef: ElementRdf
    	)
    }
    ```
    
    - 사용해 줄때는 기존 directive 사용할 때 처럼 < > 안에 selector로 만들어준 이름을 넣어서 사용!
        ![image](https://user-images.githubusercontent.com/79742210/141076213-977e6b95-df76-45c5-abd9-da964caba10e.png)

---
### .setTimeout (in Angular)

- 일정시간이 지난 후 원하는 함수를 에약 실행 할 수 있게 하는 '호출 스케줄링(scheduling a call) ( 친구로 `setInterval`이 있음)
- schedule a call
    - setTimeout > 일정 시간이 지난 후에 함수를 실행하는 방법
    - setInterval > 일정 시간 간격을 두고 함수를 실행하는 방법

- setTimeout 실행

```tsx
setTimeout('실행할부분', 1000)
setTimeout(() => '실행할부분', 1000)
	// '1000' 부분에는 원하는 시간을 적어줌
	// 실행할 부분에는 함수로 넘겨줄 수 있음
```

- 그래서 우리는 setTimeout에 if문으로 'ion-textarea' else 'ion-input'으로 input에서만 사용가능하던 directive 를 사용할수 있게되었음

---

### Page 안에서 component 가져오기

- 해당 page 안에 module을 연결해줘야 <chart> 등 가져올 컴포넌트 안에 있는 내용이 같이 보여진다
    
    Q. 그러면 현재 'admin-main.page' & dashboard 2가지 화면에서 <chart>를 보여주고 있는데 ,어떤 page에서 routing 연결을 해야하나?
    
    A :  현재 'admin-main.page' 에서 dashboard를 child로 route 연결이 되어있고, dashboard(html)안에서 <chart>를 보여주고 있으니 routing은 dashboard안에 존재해야한다
    
    - dashboard.module.ts 안에 > `chartCompModule` import 해주고,
    
         imports[ ] 안에 `chartCompMoudule` 넣어준다

---

### @Input

- 데이터를 연결해서 html로 부터 값을 받아와서 핸들링 할 수 있게 해주는 친구

---

