## chart.js

1. 우선 해당하는 HTML 파일에 <canvas> 불러고오고, 안에 지정할 id값 설정해줌
    - ex: <canvas #barChart></canvas>
2. 지정한 id값을 불러올 수 있는 함수 .ts 파일에 만들어주기! ( 1)getElementById = js 문법으로, 반영이 안된다면 2)nativeElement로 가져와보기)
    - 1) const ctx = document.getElementById('barChart');
    - 2) const ctx = (this.barChartcanvas.nativeElement as HTMLCanvasElement).getContext('2d');
    - 여기서 ctx → context의 줄임말, barChartcanvas → ViewChild로 가져오는 canvas element로 아래 참고!
3. 만들어준 함수 밑으로 chart.js 데이터 문법 넣어주기
    - new Chart 로 데이터 만들어줌
    - new Chart 안에 id로 불러온 ctx 넣어주고, 원하는 차트 type, data 등 넣어주기
    - ex: new Chart(ctx, { type: 'bar', data: { ... } })
        
![image](https://user-images.githubusercontent.com/79742210/141879521-d9b52363-a7eb-439e-8c60-cb08641343e4.png)

4. 불러온 HTML element를 ViewChild로 가져오기
    - ViewChild란? 부모 component안에 위치한 모든 자식요소들을 viewchild라고 함
    - viewchild ← component 객체, component가 랜더링 하는 view의 dom, directive 포함
    
    ⇒ 그래서 component에서 가져온 dom(여기에서는 barChartcanvas.nativeElement가 되겟지!) 을 컨트롤 해야하기때문에 ViewChild로 불러준다
    
    - ex: @ViewChild('barChart') barChartcanvas: ElementRef;
5. chart.js 보여주기

  - 이제 chart.js로 구현할 준비는 되었다. HTML에 id도 연결했고, 연결한 id값에도 chart.js data 담아줬고 이제 보여줄 부분을 만들어보자
- 구현할 data를 담아놓은 부분을 사용할 수 있게 함수로 만들어준다!
    1) drawChart( ) { } 안에 구현할 data 및 HTML에서 불러온 지정 id값 연결된 부분 담아주기
    
    ![image](https://user-images.githubusercontent.com/79742210/141879654-16085e5a-0a16-47ce-9981-1aebac071c06.png)

    2) 이제 drawChart는 사용할 수 있는 함수화가 되었다. 하지만 이거를 진짜 사용하려면 실행을 진행할 함수가 또 하나 필요하다!
        
    ![image](https://user-images.githubusercontent.com/79742210/141879668-95925701-c6df-4156-b9a8-94b64c159d0c.png)

    새로운 chartPlz라는 함수를 만들어서 drawChart()를 담아준다
        
    3) 이제 실행할 함수를 만들었고, 이거를 보여줘야한다!
        - angular에서 보여주는 부분은 ngOnInit 가 담당하기 때문에 ngOnInit안으로 넣어줘야함
        - ex: this.chartPlz();
        
        ⇒ 하지만 this로 불러오는 것 만으로는 화면을 그려줄 때, 보이지 않을때가 있어서 setTimeout으로 시간조정을 해준다
        ![image](https://user-images.githubusercontent.com/79742210/141879704-c22f4270-8458-4abd-926e-bd9080fd644f.png)

  ⇒ 요렇게 셋팅하면 현재 보여주려는 HTML + TS파일에서 보여주기가 가능하다

- chart.js 에서는 var(—ft-color)로 설정해놓은 색상값 사용 x
- `chart.register` → path 최상단(admin-main.page)에 넣어놓고 써야함/ component마다 설정 x

  
  
