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


