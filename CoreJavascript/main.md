## CoreJavascript 정리

[#1] 데이터 타입  
  
1-1 데이터 타입의 종류
- js 데이터 타입에는 기본형 primitive type & 참조형 reference type 2가지가 있음
- 기본형 = 값이 담긴 주소값을 바로 복제 vs 참조형 = 값이 담긴 주소값들로 이루어진 묶음을 가리키는 주소값을 복제
- 기본형은 **불변성**을 가짐
- Primitive Type (기본형)
> Number / String / Boolean / Null / Undefined / Symbol
- Reference Type
> Object / Array / Function / Date / RegEXp(정규표현식) / Map / Set
---
1-2 데이터 타입에 관한 배경지식  
  
1-2-1 메모리와 데이터
- bit = 0,1로 표현가능한 하나의 메모리 조각
- byte = 8개의 bit로 구성
- DATA = memory address 로 구분 & 연결 지음
  
1-2-2 변수 & 식별자
- 변수 = '변할 수 있는 수'로 변할 수 있는 무언가로 해석 (무언가 = data)
- 식별자 = 변수명, 어떤 데이터를 식별하는데 사용하는 이름
---
1-3 변수 선언과 데이터 할당  
  
1-3-1 변수 선언
- ex 1)
```html

var a;

```
> ex 1) 을 말로 풀면 "변할 수 있는 데이터를 만든다. 이 데이터의 식별자는 a로 한다".  
> 변수란? 변경 가능한 데이터가 담길 수 있는 공간이라는 듯이 된다.  
> var a 라는 명령을 받은 com은 비어있는 임의로 비어있는 공간 하나를 확보하고 이 공간의 이름(식별자)를 a라고 지정한다.  
> = 여기까지가 변수 선언 과정
  
1-3-2 데이터 할당
