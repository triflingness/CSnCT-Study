# DOM
> 문서 객체 모델, Document Object Model

DOM은 XML이나 HTML 문서의 객체를 계층으로 표현하여 접근할 수 있도록 해주는 API(인터페이스)입니다.

- DOM을 이용하여 문서의 내용, 구조, 스타일에 접근하고 변경합니다.
- 스크립트 언어가 클라이언트 사이드 상호작용으로 웹페이지를 만드는데 있어 DOM은 자바스크립트가 문서 내의 모든 요소를 정의하고 각 요소에 접근하는 방법을 제공합니다.
- 문서 전체 내용이 해석되어 메모리에 저장이 되어야하기 때문에 DOM은 문서 요소가 임의적으로 접근되고 변경할 수 있어야 하는 응용 프로그램에 가장 적합합니다.
- WC3의 표준 객체 모델입니다.

### 트리 계층 구조로 표현됩니다.

![Untitled](https://github.com/triflingness/CSnCT-Study/blob/main/IT%20Common%20Sense/images/DOM.png)

자바스크립트는 이러한 객체 모델을 이용하여 다음과 같은 작업을 할 수 있습니다.

- 자바스크립트는 `새로운 HTML 요소나 속성을 추가`할 수 있습니다.
- 자바스크립트는 `존재하는 HTML 요소나 속성을 제거`할 수 있습니다.
- 자바스크립트는 HTML 문서의 `모든 HTML 요소를 변경`할 수 있습니다.
- 자바스크립트는 HTML 문서의 `모든 HTML 속성을 변경`할 수 있습니다.
- 자바스크립트는 HTML 문서의 `모든 CSS 스타일을 변경`할 수 있습니다.
- 자바스크립트는 HTML 문서에 `새로운 HTML 이벤트를 추가`할 수 있습니다.
- 자바스크립트는 HTML 문서의 `모든 HTML 이벤트에 반응`할 수 있습니다.

## 예시

```html
<!DOCTYPE html>
<html lang="en">
<head>
<title>Event Propagation</title>

<style>
#t-daddy { border: 1px solid red }
#c1 { background-color: pink; }
</style>

<script>
function stopEvent(ev) {
  c2 = document.getElementById("c2");
  c2.innerHTML = "hello";

  // this ought to keep t-daddy from getting the click.
  ev.stopPropagation();
  alert("event propagation halted.");
}

function load() {
  elem = document.getElementById("tbl1");
  elem.addEventListener("click", stopEvent, false);
}
</script>
</head>

<body onload="load();">

<table id="t-daddy" onclick="alert('hi');">
  <tr id="tbl1">
    <td id="c1">one</td>
  </tr>
  <tr>
    <td id="c2">two</td>
  </tr>
</table>

</body>
</html>
```

## DOM의 종류

W3C DOM 표준은 3가지 종류가 있습니다.

1. Core DOM : 모든 문서 타입에 접근할 수 있는 DOM 모델
2. HTLM DOM : HTML 문서를 위한 DOM 모델
3. XML DOM : XML 문서를 위한 DOM 모델

### HTML DOM

HTML 문서를 조작하고 접근하는 표준화된 방법을 정의합니다.

HTML요소는 HTML DOM에 접근할 수 있습니다.

### XML DOM

XML DOM은 XML 문서에 접근하여, 그 문서를 다루는 표준화된 방법을 정의합니다.

모든 XML 요소는 XML DOM를 통해 접근할 수 있습니다.

---

[http://www.tcpschool.com/javascript/js_dom_concept](http://www.tcpschool.com/javascript/js_dom_concept)
