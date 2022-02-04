
### Javascript
---

### Class - property & method

- 객체 지향 프로그래밍 → 인터페이스 구분 → '내부 인터페이스' & '외부 인터페이스'
    - 내부 인터페이스(interal interface) : 동일한 클래스 내의 다른 메소드에서는 접근이 가능하지만, 클래스 밖에서는 접근 불가능
    - 외부 인터페이스(external interfacd) : 클래스 밖에서도 접근 가능한 프로퍼티 & 메소드

- javascript의 인터페이스!
    - public
    - private
    - protected → public & private 의 중간? 위로부터 상속받아오는 class 중에 접근이 가능하도록 하려면 protected를 사용
        
        (private 는 상속자의 관계여도 접근이 되지 않기 때문!)
        
        ( javascript 에서는 protected 를 정식 지원 x , but 사용하면 편리한 점이 많기때문에 이를 따와서 사용하는 경우 ⬆️  )

---

### Primitive type & Reference type

- primitive ⇒ 메모리 공간에 변수가 가지는 값 자체를 저장 : 실제 데이터 값을 저장하는 타입
- reference ⇒ 객체가 저장되어있는 위치를 저장 : 메모리 번지 값을 통해 객체를 참조하는 타입

- primitive(원시 타입)
    - 정수 : byte, short, int, long
    - 실수 : float, double
    - 문자형 : char
    - 논리형 : boolean
- reference(참조 타입)
    - class, interface, array 등

- 차이점
    1. 원시타입은 null을 담을 수 없지만, 참조타입은 가능
    
    ```java
    int i = null //불가능
    Integer integer = null //가능
    (integer = wrapper class)
    ```
    
    1. 원시타입은 제너릭 타입에서 사용할 수 없지만, 참조타입은 가능

- Boxing & Unboxing
    - Boxing : 원시타입을 참조타입으로 변환시켜줌
    - Unboxing : 참조타입을 원시타입으로 변환시켜줌

---
### JS 일급함수

- javascript에서 객체는 일급객체
- javascript의 함수는 일급함수
- 함수 또한 객체로 표한하기 때문에 일급 함수도 만족

⇒ 함수를 변수에도 할당할 수 있고, 객체에 추가할 수도 있고, 다른 함수에 인수로 전달하거나 함수에서 함수를 반환할 수 있음

- First Class Citizen(일급 시민)
    1. 변수에 담을 수 있다
    2. 인자로 전달할 수 있다
    3. 반환값으로 전달 할 수 있다

- First Class Object(일급객체)
    
    : 객체를 일급 시민으로 취급
    

⇒ 변수나 데이터에 할당 가능, 인자로 넘기기 가능, 리턴값으로 리턴하기 가능

- First Class Funciton(일급함수)
    
    : 함수를 일급 시민으로 취급 → 함수를 값으로 다룰 수 있음 (함수 스스로 객체로 취급해버리는거)
    

⇒ 함수가 다른 일급 객체에서 동일하게 다루어질때, 일급함수라 부름

```jsx
//변수에 할당 -> 변수를 사용해 호출
const abc = function() {
	console.log('abcFunc');
}
abc();

//인자로 전달 -> 'function 'hello'를 function 'world'에 인자로 전달
function hello() {
	return "Hello";
}
function world(helloMsg, name) {
	console.log(helloMsg() + name);
}
world(hello, 'hi');

//함수를 반환
function sayHello() {
	return function() {
		console.log('say hi')';	}
}
```
---

### 객체지향 vs 함수지향
함수지향 프로그래밍 → 순수함수 & 아닌함수

객체지향 프로그래밍 → class로 컨트롤

---

### 참조타입 다른 주소로 바라보게하기

- [원시타입 과 참조타입 ?](https://www.notion.so/IONIC-memo-45e54490496b4b3ca2e8f4f328b47135)

⇒  원시타입이 아닌 참조타입은 값을 할당하는 방식이 아니라, 담아져있는 주소를 할당하는 방법으로 값을 전달하는데 이러한 방식을 angular에서는 인지하지 못하는 현상이 있음

const a = {a:1, b:2}

a = 4q5423qw → a의 주소가 요렇게 할당되어 있을때

const c = a 로 선언을 하게되면

c = 4q5423qw → c도 같은 주소를 바라보게 된다 → 그러면 값을 복사한게 아니라 해당 주소를 복사해서 가지고 있다고 보면되고

이러한 방식일때

c에서 값을 수정했을때 a의 값도 바뀌어야하는데 angular에서는 같은 주소를 가지고 있다고 판단하여 값을 바꾸어주지 않는다

이럴때 아래 3가지의 방식을 사용하면 a와 c는 서로 다른 주소를 가지고 있게 된다.

1. _.cloneDeep
2. 구조분해 ( a = {...a})
3. Object.assign({ }, a) → 빈배열에 a를 넣어버리는 방식

---

### splice 함수 → javascript

- splice → javascript 배열(Array)객체에서 제공하는 함수
- splice 는 추가 & 삭제가 모두 가능
    
    ```jsx
    const a = ['A', 'B', 'C', 'D', 'E']
    
    a.splice(2, 0, '7'] //2번 index로부터 0번째 자리에 '7'를 추가
    => const a = ['A', 'B', '7', 'C', 'D', 'E']
    
    a.splice(0, 0, '1'] //0번 index로부터 0번재 자리에 '1'추가
    => const a = ['1', 'A', 'B', '7', 'C', 'D', 'E']
    
    a.splice(2, 1) //2번 index로부터 1개를 삭제
    => const a = ['1', 'A', '7', 'C', 'D', 'E']
    ```
    
---

