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
