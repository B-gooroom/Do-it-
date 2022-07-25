## prototype ?

- protoytpe = 원형
- 이로인해 js는 '상속'이라는 개념을 가지고 감

<br>
  <img width="400" alt="스크린샷 2021-11-21 오후 1 15 16" src="https://user-images.githubusercontent.com/79742210/142749368-9fe8a16a-71f0-4993-a051-06ae825c5fb1.png">
- 이렇게 3가지의 값이 주어졌다고 했을때, 마지막 console.log(o.ultraPop)의 접글하여 로그를 찍게되면 어떻게 될까?

1. js에서는 단계별로 상속되고 있는 곳으로 올라가서 값을 가져오게 된다.
2. 마지막 `var o = new Sub();` 이라고 했을때,
 -> var o 는 'function Sub()'의 값을 가지고 있게 되는데 -> Sub은 Super의 prototype이고, 또 Super는 Ultra의 prototype이다.
3. 3가지의 값중 가장 최상위에 있는 `function Ultra` 안 에 `'Ultra.prototype.ultraProp = true'`라는 선언이 존재한다.
4. 해서 Ultra -> Super -> Sub, var o = Sub 까지 상속의 형태를 띄고, var o는 최상의 상속자로 접근해 ".ultraProp"의 값을 log로 찍어낼 수 있게 된다.

- 생성자 = 기본적으로 함수
- 앞에 붙여주는 'new'로 생성자 함수가 되고,
- 그렇게 실행된 결과 => 새로운 객체를 만들어서 그 객체 자체를 return하게 한다.
<br>
=> 위 예제처럼 타고타고 올라가는 것을 `"prototype Chain"`이라고 부른다.<br>
=> 객체를 만들었을때, 그 객체가 가지고 있어야하는 데이터(property)까지 넘겨주기를 원하기 때문에 생성자 함수를 사용하게 된다.<br>
=> 우리가 쓰고자 하는 그 객체들은 어딘가에 저장되어 있는데, 쓰고 싶을때 `'new'`로 꺼내오게 되면 쓸 수 있다.

---

