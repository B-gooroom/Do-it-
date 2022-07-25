## CSS_grammar

### 문법
* 선택자 = selector
* 속성 = property ; 
* 값 = value
* 선언 = declaration
* 선언부 = {}
* 규칙 = rule set
* 주석 = /* ~ */

### 적용방식
* inline <div style=  > 내용 </div> (자주사용x)
* internal <style> ... </style>
* external <링크태그> link rel = stylesheet href='css/style.css' (주로 사용함)

### id 선택자
* css = #(id이름) {font-size: 30px;}(속성입력)
* html = 태그 안에서 id값(이름) 지정

### class 선택자
* css = .(class이름) {font-size: 30px;}(속성입력)
* html = 태그 안에서 class값(이름) 지정

### display
* display = 객체들을 어떤 방향으로 어떻게!
* 기본 html > 좌측 상단부터 객체 생성
1. block - 아래로 쌓임(객체단위(box))
3. inline - 우측으로 쌓임/ width,height 값 적용x
4. inline-block - 우측으로 쌓임(객체단위(box))
5. none - 화면상에서 제거

### cascading(우선순위적용)
- inline style > id > class > 시멘틱(기본속성태그)
* 1개의 태그 여러가지 값을 지정한 경우 = 가장 마지막에 적용된 스타일 속성이 win!
* ⌘ + ⌥ + i = elements 창 > style 창에서 적용된 우선선위 확인
