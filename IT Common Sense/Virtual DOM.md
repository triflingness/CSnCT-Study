## DOM의 렌더링 방법

<p>
  <img src="https://github.com/triflingness/CSnCT-Study/blob/main/IT%20Common%20Sense/images/Rendering.png">
</p>

브라우저는 DOM을 이용하여 화면을 렌더링합니다.

- DOM Tree 생성) 브라우저는 HTML을 파싱하여 html 태그로 이루어진 각 노드로 DOM Tree를 만듭니다.
- Render Tree 생성) CSS 파서를 이용한 Style Rules를 DOM Tree와 합쳐 Render Tree를 만듭니다.
    - 'Attachment'는 노드의 스타일을 처리하는 과정입니다. 각 노드는 동기적으로 'attach'라는 메소드를 가지고 있어 스타일 정보를 계산해서 객체 형태로 반환합니다.
- Layout) Render Tree가 만들어지면 각 노드들은 화면의 좌표가 주어지고 위치가 정해집니다.
- Painting) Render Tree를 돌며 각 노드의 paint()메소드를 호출합니다. 구현된 화면이 출력이 됩니다.

여기서 DOM은 변화가 생기면 Render tree를 재생성하고 레이아웃을 만들고 페인팅하는 과정을 반복합니다.

Render tree가 재생성될 때는 모든 요소들의 스타일이 다시 계산됩니다.

따라서 한 개의 변화가 레이아웃 변화, 트리변화, 렌더링을 일으킵니다.

예를 들어 30개의 변화가 생기면 30번 렌더링 과정을 해야합니다. 이는 불필요한 연산까지 포함하고 있어 비효율적입니다.

## Virtual DOM

> 가상의 DOM 형태

Virtual DOM은 여러 개의 수정사항을 모아서 실제 DOM이 한 번만 렌더링을 할 수 있게 해줍니다.
실제 DOM에 적용되기 전에 Virtual DOM에 먼저 적용시켜 최종적인 결과만 브라우저에게 전달해줍니다.
이는 브라우저의 연산과정을 줄여 시간을 줄이고 성능을 향상시킬 수 있습니다.

<p>
  <img src="https://github.com/triflingness/CSnCT-Study/blob/main/IT%20Common%20Sense/images/Virtual%20DOM.png">
</p>

---

[https://velopert.com/3236](https://velopert.com/3236)

[https://www.howdy-mj.me/dom/what-is-dom/](https://www.howdy-mj.me/dom/what-is-dom/)
