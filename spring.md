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
#### web

- 정적 컨텐츠 → server에서 그대로 출력  
    `resources > static > 만든 html 파일을 그대로 웹 브라우저에 출력`
    1. router [hello-static.html](http://localhost:8080/hello-static.html)([localhost:8080/hello-static.html](http://localhost:8080/hello-static.html)) 입력
    2. tomcat이 ‘hello-static’ 이름의 controller 검색 (controller 먼저 찾아봄, 우선순위 ↑)
    3. `resources: static/hello-static.html` 로 찾아서 출력해줌
- mvc & 템플릿 엔진 → jsp, php처럼 html을 동적으로 바꿔서 출력
    - 서버에서 변형해서 출력
    - mvc : Model, View, Controller
    - controller 와 view는 나누어서 setting
- api  
    `json 형식 또는 string 형식으로 데이터 구조 포맷으로 클라이언트에게 출력해주는 방식`
    1. controller → @ResponseBody (ResponseBody가 return 해주면 HttpMessageConverter가 작동함)
    2. HttpMessageConverter → 단순 문자면 StringConverter/ json 이면 JsonConverter
    3. json은 요청한 웹 브라우저에게 던져주고 출력됨
    
<!--     <aside> -->
> 📌 @ResponseBody를 사용하면 `viewResolver` 대신 `HttpMessageConverter`가 동작  
> - 문자 → `StringHttpMessageConverter`
> - 객체(json) → `MappingJackson2HttpMessageConverter`
> (Jackson ⇒ 객체를 json으로 바꿔주는 대표적인 lib, spring은 Jackson을 가지고 있음)
    
<!--     </aside> -->

---
#### spring의 동작

1. controller : 외부 요청 받고
2. service : 비즈니스 로직 만들고
3. repository : 데이터 저장해주고

> 📌 스프링 컨테이너  
> helloController → memberService → memberRepository

- 스프링 bean을 등록하는 2가지 방법
    - 컴포넌트 스캔(@Controller, @Service, @Repository)과 자동 의존관계 설정
        - @Component 애노테이션이 있으면 스프링 빈으로 자동 등록됨
    - 자바코드로 직접 스프링 빈 등록
        - 설정파일(SpringConfig)에 등록
- 스프링은 컨테이너에 빈을 등록할 때, `싱글톤`으로 등록(하나만 등록하여 공유해서 사용해야함)

- **DI(Dependency Injection)**
    - 생성자 주입
    <img width="400" alt="스크린샷 2023-03-05 오후 5 30 53" src="https://user-images.githubusercontent.com/79742210/229024691-5a6598f3-eb39-4464-8c46-831d6b4060e8.png">

    - 필드 주입
    <img width="350" alt="스크린샷 2023-03-05 오후 5 28 56" src="https://user-images.githubusercontent.com/79742210/229024857-17cc1c23-292a-4015-9f57-d4fb66f91270.png">

    - setter 주입
      - 단점 = public으로 열어둬야함(노출됨)
    <img width="400" alt="스크린샷 2023-03-05 오후 5 28 09" src="https://user-images.githubusercontent.com/79742210/229024905-a2a950dd-0e4c-418e-a667-c11a021ec285.png">

---
#### JDBC

- 개방-폐쇄 원칙(ocp, Open-Closed Principle)
    - 확장에는 열려있고, 수정 & 변경에는 닫혀있음
- 기존 코드를 만지지않고, 구현 클래스를 변경할 수 있음
- `@SpringBootTest` - 스프링 컨테이너와 테스트를 함께 실행
- `@Transactional` - 테스트 시작 전에 트랜잭션을 시작하고, 완료후 항상 롤백 → 다음테스트에 영향을 주지 않음

---
#### JPA (Java Persistence API)

*myBatis > jpa (국내), 

- 기존의 반복코드, 기본적인 sql도 직접 만들어서 실행해줌
- 객체 중심의 설계로 생각해볼 수 있음
- 개발 생산성을 크게 높을 수 있음

---
#### 스프링 데이터 JPA

- JPA 프레임워크
    - repository 구현 클래스 없이 인터페이스 만으로도 개발이 가능함
    - 기본 CRUD 기능도 스프링 데이터 JPA가 모두 제공
    - 관계형 데이터베이스를 사용한다면 스프링 데이터 JPA는 필수!
    - 공통화 메서드를 기본적으로 제공해줌 → 메서드 이름만으로 조회 기능 제공
        - `findAll()`
        - `findById()`
        - `findAllById()`
        - 등등..
- 실무에서는 JPA & 스프링 데이터 JPA를 기본적으로 사용, 복잡한 동적 쿼리는 Querydsl 라이브러리 사용
    - Querydsl → 쿼리도 자바 코드로 안전하게 작성 가능, 동적 쿼리도 편리하게 작성할 수 있음!
    - or JPA 네이티브 쿼리
    - or JdbcTemplate

---
#### AOP(Aspect Oriented Programming)

- `공통 관심 사항(cross-cutting concern)` vs `핵심 관심 사항(core concern)` 의 분리 (프론트의 컴포넌트화로 이해)
    - 시간을 측정하는 로직은 `공통 관심 사항`
    - 실제로 동작하는 로직은 `핵심 관심 사항`
