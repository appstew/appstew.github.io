[mermaid.js 사이트 포크](https://github.com/appstew/mermaid/tree/develop/docs)

- 아이패드 사파리에 켜놓은 것 보고 실습

<details>
<summary>메모한 글</summary>
- obsidian
  - 플러그인, 테마 등
  - 처음 러닝커브만 지나면 노션보다 훨씬 낫고 좋다고?
  - 컴퓨터에서도 한번 써봐야겠다. 
  - [markdown monster](https://markdownmonster.west-wind.com/docs/_5ef0x96or.htm) 발견.
  

- 깃헙 블로그는 csr? ssr? 
  - 이게 생각보다 어렵다. 구글에서 ssr csr 차이 예시 구분 방법 등 한글로 검색해보아도, 나오든 거의 모든 글들이 똑같은 내용만 담고 있다..
  네이버 블로그는 2020년부터 ssr 로 전환했다는 것만 어디서 확인했을 뿐, ssr, csr 이론적인 설명 차이 등만 있고 구체적으로 무슨 사이트가 정확히 csr 이다 ssr 이다 하는 설명은 찾을 수 없었다.
  - 또한 정적 웹사이트는 csr, 동적 웹사이트는 ssr 이라고 하지만 여전히 해깔린다..
  - 한가지 확실한 것은 가령 stendhal 같은 자바 웹 게임은 분명 csr 일 것이다.
  - 아무튼 혹시 몰라 영어로 검색해보았다. [이 글](https://stackoverflow.com/questions/62329411/how-to-see-whether-a-website-is-client-side-rendered-or-server-side-rendered) 에서 말하길, 
  - "현실적으로, ssr 과 csr 사이에 뚜렷한 구분법은 없다. 대부분 csr 이라 부를 웹사이트도 여전히 서버로 html 을 전송할 것이다. 때로는 엄청 많은 양을. 그리고 대부분 ssr 이라 부를 웹사이트도 여전히 유저입력에 따라 약간의 html 수정이 발생한다."
  - "브라우저에서 view source 와 관리자도구의 element inspector 안의 내용이 완전히 동일하면, 이는 100% SSR.  
  약간의 차이가 있으면 약간 csr 적이고, 차이가 크다면 ssr 보다는 csr 에 가깝다고 볼 수 있다."
  - ctrl+U 로 소스에서 코드 양이 적으면 csr, 이미 (거의) 모든 컨텐츠를 갖고 있다면 이는 ssr.
  - 실제로 stendhal game 은 소스의 양이 291페이지밖에 안되고 csr임을 다시 확인할 수 있다.
  - 가령 built 데이터로 구동하는 깃헙 블로그와 velog의 경우, 페이지마다 소스 코드가 바뀌고, 그 페이지에서 필요한 모든 코드를 각 소스에 가지고 있는 것을 보아 ssr 인듯. 그럼 벨로그나 깃헙 블로그가 동적 블로그라고?
  - stendhal game 은 역시 장소를 이동해도, 소스코드가 계속 동일하고 짧다. 그래서 csr임이 다시 확인되지만, 정적 웹사이트라고?

- 아무튼 CSR 과 SSR 을 어느정도 구분은 할 수 있을 것 같다.
  - 나중에 정적 웹사이트 vs 동적 웹사이트 에 대해 좀 더 알아보자.
  - 그런데, 가령 github pages 가 SSR, 즉 server-side-rendering 인데, 조금 전에 파이어폭스에서 mermaid renderer 애드온을 깔은 후에야 비로소 mermaid charts 가 렌더링 되는 것은 왜일까? 어떻게 이해해야 할까?


- github pages 는 SSR 이고 mermaid.min.js 까지 제공하는데 왜 크롬과 파폭 등 브라우저 단에서는 렌더링 애드온이 필요한 걸까?
  - [kiroki.io](https://kroki.io/)
    - [cheat sheet](../../img/fedora_hrd/kroki.io_printPDF.pdf)
      - Excalidraw[]
      - Graphviz
      - [PlantUML](https://plantuml.com/starting)
  - https://gojs.net/latest/intro/ 여기서 나중에좀 천천히 읽고 실습해보자.
  - about:debugging#/runtime/this-firefox 에서 Markdown Diagrams 소스코드, 디버깅툴 보기
  - 그리고 schema, 자료구조 시각화 자료 등, 시간 날때 알아보자.
  - markdownMonster
  - Obsidian
  - [intelliJ Diagram exmaple](../../img/fedora_hrd/beandiagram.svg)
    - <details>![](../../img/fedora_hrd/beandiagram.svg)
    </details>



</details>



## 220824 
- 인텔리제이로 Downloads 안에 [mermaid.site](https://github.com/appstew/mermaid) [GoJS.site](https://github.com/appstew/GoJS) 를 열어보았고, 인텔리제이로도 자바 뿐만 아니라 다른 것들도 할 수 있다는 것을 알게되었다.
  - mermaid.site 와 GoJS.site 각각 포크하였다.
mermaid.site 의 경우
  - 파이어폭스의 렌더 엔진을 꺼도 보기좋지는 않지만, 어쨋든 md 문서의 mermaid-example 들이 렌더링 되긴 하는 것을 알게 되었다. 
  - .nojekill 파일이 있고, [docify블로그프레임워크](docsify.js.org/#/ssr)를 사용하고 있다는 것을 알게 되었다. 또한, docify 사이트 안에 SSR 을 위시한 설명이 있고 어떻게 mermaid 를 렌더링 했는지 좀 더 알아보자.

- 그리고, 나무위키에 다음을 검색한 내용과 진도 공부 내용 등을, croki 등 goJS 든 어디서든 간에 빨리 다이어그램으로 정리하자.
  - 그렇게 하지 않으면 머리에 정리도 안되고, 기억에 아무것도 안 남을 것 같다.
- 더 알아볼거 
  - webpack
  - nodeJS, 웹프레임워크, ruby, 
