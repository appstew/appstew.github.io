
https://github.com/appstew/mermaid/tree/develop/docs

# 질문 내용

1. 제가 깃헙블로그를 하다가 mermaid 라는 차트에 관심이 생겼고 마크다운에 다음과 같이 쓰면 빌드된 웹페이지(html과 js 파일 경로 등) 에 렌더링이 된다고 해서 작동하게 하려고 처음에 애를 썼었습니다.

다음과 같이 쓰면 

```
//```mermaid
graph TD; A-->B; A-->C; B-->D; C-->D; click D href "https://google.com" 
//```
```
![](https://kroki.io/mermaid/svg/eNpLL0osyFAIcbHmUgACR11dOycE0xnCdAIyoQqcIczknMzkbAUXhYyi1DQFpYySkoJiK3399Pz89JxUveT8XCUAXt8V4A%3D%3D)

이렇게 나와야 하고 

https://appstew.github.io/posts/mermaid.working/
이게 머메이드 차트만 모아서 정리한 제 블로그입니다. 

2. 그런데 제가 파이어폭스를 쓰는데 제 블로그에 접속해도 렌더링이 되지 않았습니다. 


<details>
<summary>메모한 글</summary>
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
</details>

```html
      <!--
  mermaid-js loader
-->

<script src="https://cdnjs.cloudflare.com/ajax/libs/mermaid/9.1.6/mermaid.min.js"></script>

<script>
  $(function() {
    function updateMermaid(event) {
      if (event.source === window && event.data &&
            event.data.direction === ModeToggle.ID) {

        const mode = event.data.message;

        if (typeof mermaid === "undefined") {
          return;
        }

        let expectedTheme = (mode === ModeToggle.DARK_MODE? "dark" : "default");
        let config = { theme: expectedTheme };

        /* Re-render the SVG › <https://github.com/mermaid-js/mermaid/issues/311#issuecomment-332557344> */
        $(".mermaid").each(function() {
          let svgCode = $(this).prev().children().html();
          $(this).removeAttr("data-processed");
          $(this).html(svgCode);
        });

        mermaid.initialize(config);
        mermaid.init(undefined, ".mermaid");
      }
    }

    let initTheme = "default";

    if ($("html[data-mode=dark]").length > 0
      || ($("html[data-mode]").length == 0
        && window.matchMedia("(prefers-color-scheme: dark)").matches ) ) {
      initTheme = "dark";
    }

    let mermaidConf = {
      theme: initTheme  /* <default|dark|forest|neutral> */
    };

    /* Markdown converts to HTML */
    $("pre").has("code.language-mermaid").each(function() {
      let svgCode = $(this).children().html();
      $(this).addClass("unloaded");
      $(this).after(`<div class=\"mermaid\">${svgCode}</div>`);
    });

    mermaid.initialize(mermaidConf);

    window.addEventListener("message", updateMermaid);
  });
</script>
```
