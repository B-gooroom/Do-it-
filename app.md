
### ios App LifeCycle

- Not Running - 아무것도 실행하지않은, 앱을 키지 않았거나 종료한 상태
- Inactive - active 상태에서 추가 작업을 하는 상태
- Active - 앱이 켜져 있는, 이벤트를 받을 수 있는 상태
- Background - 앱을 껏지만 뒤에 남아있는 상태

> 13부터는 이름이 변경
- willFinishLaunching
    - didFinish 전에 호출되는 함수
- didFinishLaunching
    - 앱 실행시 1번만 실행되는 함수
- applicationDidBecomeActive
    - active 상태 직후
    - 화면으로 돌아올 때마다  실행
- applicationWillResignActive
    - actice → inactive 상태로 전환시
    - 아래 상황들은 Background로 넘어가지 않는다! (active → inactive → active)
      - 반만 올려서 여러앱들이 떠있는 상태(최소화)
      - 전화가 올 때
      - 문자가 오고 문자를 확대했을 때
      - 왼쪽상단 스크롤 → 알림센터를 열었을 경우
      - 오른쪽 상단 스크롤 → 제어센터를 열었을 경우
- applicationDidEnterBackground
    - background 상태전환 직후
- applicationWillEnterForeground
    - background → foreground 상태로 전환시 foreground 직전
- applicationWillTerminate
    - 앱 종료시
---

> 앱 open -> close 상태 변화

1. 앱을 키기 위해 앱을 누른다 → willFinishLaunching

2. 앱으로 진입 → didFinishLaunching

3. 앱으로 진입 완료 (그래서 드디어 앞에 application이 붙는다!) → applicationDidBecomeActive

---_앱을 실행해 active상태로 가게되면 기본적으로 여기까지 진행됨._--- <br><br>

--- _앱이 실행된 상태에서 이렇게 저렇게 시도하는 경우_---

4. 앱이 실행중에 제어/알림센터 내리거나 홈키로 여러앱을 띄워놓은 상태일 경우 → applicationWillResignActive

5. 잠깐 홈키를 눌러서 홈화면으로 이동했다 → applicationDidEnterBackground

6. 다시 앱으로 컴백 → applicationWillEnterForeground

7. 앱을 종료합니다 → applicationWillTerminate

