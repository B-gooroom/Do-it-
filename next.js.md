## Next.js
 - React + 
- Express.js + 
- React-Router-Dom + 
- Server Side Rendering
- React의 프레임워크
---

### SSR(_Server Side Redering)

- SSR에서의 Rendering ?
> html을 어디서 주고 있는가??  
→ html에 내용이 있는가 없는가가 요지
>

> 
> 
1. Server Sending Ready to be rendered HTML Response to Browser
2. Browser Renders the page. `Now Viewable`
3. And Browser Downloads JS files, Browser executes React
4. Page `Now Interactable`

> 렌더가 될 준비가 된 html을 broswer에 뿌리기때문에 바로 볼 수가 있음  
그 후 js 파일을 실행  
완전히 끝난후에 기능까지 동작 가능(상호작용)
>
⇒ SSR에서는 렌더가 될 수 있는 html을 먼저 그려주기 때문에, 2단계에서부터 화면을 볼 수 있다.
(기능보다 화면이 먼저 그려짐)
