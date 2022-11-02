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
---

### pages
- Next는 pages 폴더 하단에 있는 페이지 경로,이름 그대로를 url 경로로 라우팅 해줌
- 파일 이름
  - 파일의 이름이 url로 적용되려면 `export default function 파일이름 () {}`으로 설정해주어야 따라갈 수 있음
  - 파일 이름 = url pathname 이므로 신중히 결정할 것
- pages 하단에 자리하는 index파일 -> route ('/'), '홈'화면의 역할을 해줌

---
### routes with <Link>
 - Next에서는 pages에서 말했듯이 `auto routing`을 지원해줌 -> 기존 React에서는 페이지 이동을 위해서 route를 연결해주고 불러서 사용
 - <Link> 태그를 이용하여 이동하도록 구현
 
 ``` 
import Link from 'next/link';

export default function NavBar() {
	return (
		<div>
			<Link href="/">홈</Link>
			<Link href="/details">상세페이지</Link>
		</div>
	)
}
```
 - Next에서는 <Link> 태그안에서 href="/라우터이름"으로 적용해야함


