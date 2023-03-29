### Spring

---
#### install
```
https://start.spring.io/
```
- project : `Gradle`
- Language : `Java`
- Spring Boot : `2.7.9`(snapshot = 정식x)
- Project Metadata
  - Group : `kr.bunny`
  - Artifact : `bunny-spring`
  - Name : `bunny-spring`
  - Description : Demo project for Spring Boot
  - Package name : `kr.bunny.bunny-spring`
  - Packaging : `Jar`
  - Java : `11`

---
#### run
*src > java > kr.bunny.bunnyspring > `BunnySpringApplication`
```
▶️ BunnySpringApplication
```
- `http://localhost:8080`으로 동작 확인

---
#### build & run
*bunny-spring(root)
```shell
./gradlew build
```
- `http://localhost:8080`으로 동작 확인
</br>
  
*bunny-spring > build > libs
```shell
java -jar bunny-spring-0.0.1-SNAPSHOT.jar
```
</br>
  
🚧 한번에 실행되지 않을 때 -> build 파일 청소 후 다시 실행
```
./gradlew clean build
```
</br>
  
```
🔑 서비스 실행 시 생성된 jar 파일 서버에 업로드해서 사용
```
---

#### spring의 lib
- init 시 선택한 lib는 thymleaf, spring-web 뿐인데 열어보니 내장 라이브러리가 많다?
  - Gradle || Maven -> 기본적으로 의존형태를 띄고 있는 라이브러리를 가져옴
</br>
  
- spring-boot-starter-web
  - spring-boot-starter-tomcat : 웹서버
  - spring-webmvc
- spring-boot-starter
  - spring-core
  - logging
    - logback
    - slf4j
- test용
  - junit(ver.5)
  - spring-test

---
#### view
> controller : '클라이언트'로부터 요청 받기 </br>
> model : 페이지에 쓰일 데이터 전달 (react에서 하위 컴포넌트에게 props 전달과 유사함) </br>
> view : 받아온 테이터로 페이지 그려주기 </br>
  
`controller -> view & model을 연결시켜 주는 라우팅 역할`
  
<img width="920" alt="스크린샷 2023-03-02 오전 11 20 41" src="https://user-images.githubusercontent.com/79742210/222317112-86fc5756-4779-4378-93eb-c216a21774b9.png">
  
```shell
1. router에 'localhost:8080/hello' 입력
2. tomcat이 'hello'라는 이름으로 가져올 수 있는 controller로 접근 -> HelloController
3. HelloController는 model에 ('data'라는 key, 'hello!'라는 value)를 넣어두고 'hello'로 return
4. resources/templates에 'hello(hello.html)' 파일을 찾음
5. hello.html에 model을 전달하고 이를 출력
```
- viewName Mappging
  ```java
  'resources:templates' + {viewName}.html`
  ```

---
### web

- 정적 컨텐츠 → server에서 그대로 출력
    - resources > static > 만든 html 파일을 그대로 웹 브라우저에 출력
    1. router [hello-static.html](http://localhost:8080/hello-static.html)([localhost:8080/hello-static.html](http://localhost:8080/hello-static.html)) 입력
    2. tomcat이 ‘hello-static’ 이름의 controller 검색 (controller 먼저 찾아봄, 우선순위 ↑)
    3. `resources: static/hello-static.html` 로 찾아서 출력해줌
- mvc & 템플릿 엔진 → jsp, php처럼 html을 동적으로 바꿔서 출력
    - 서버에서 변형해서 출력
    - mvc : Model, View, Controller
    - controller 와 view는 나누어서 setting
- api
    - json 형식 또는 string 형식으로 데이터 구조 포맷으로 클라이언트에게 출력해주는 방식
    1. controller → @ResponseBody (ResponseBody가 return 해주면 HttpMessageConverter가 작동함)
    2. HttpMessageConverter → 단순 문자면 StringConverter/ json 이면 JsonConverter
    3. json은 요청한 웹 브라우저에게 던져주고 출력됨
    
<!--     <aside> -->
> 📌 @ResponseBody를 사용하면 `viewResolver` 대신 `HttpMessageConverter`가 동작  
> - 문자 → `StringHttpMessageConverter`
> - 객체(json) → `MappingJackson2HttpMessageConverter`
> (Jackson ⇒ 객체를 json으로 바꿔주는 대표적인 lib, spring은 Jackson을 가지고 있음)
    
<!--     </aside> -->

