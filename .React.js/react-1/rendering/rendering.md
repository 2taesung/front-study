# Rendering 원리

### React 에서 Rendering의 정의

React에서 렌더링이란 <mark style="background-color:green;">render() 함수</mark>를 사용하여 페이지를 리디렉션할 수 있는 기술.

```javascript
const RootNode = document.getElementById('root');
const Root = ReactDOM.createRoot(RootNode);
Root.render(React.createElement(element));
```

```javascript
const element = {
  type: "h1",
  props: {
    title: "foo",
    children: "Hello",
  },
}

const container = document.getElementById("root")
const node = document.createElement(element.type)
node["title"] = element.props.title

const text = document.createTextNode("")
text["nodeValue"] = element.props.children
node.appendChild(text)
container.appendChild(node)
```

### 렌더링의 큰 과정

1. 기존 컴포넌트의 UI를 재사용할 지 확인한다.
2. 함수 컴포넌트: 컴포넌트 함수를 호출한다 / Class 컴포넌트: `render` 메소드를 호출한다.
3. 2의 결과를 통해서 새로운 VirtualDOM을 생성한다.
4. Reconciliation(재조정) : 이전의 VirtualDOM과 새로운 VirtualDOM을 비교해서 실제 변경된 부분만 DOM에 적용한다.

먼저 4번의 과정을 왜 하는지, 근본적으로 VirtualDOM을 왜 사용하는지에 대해 알아보겠습니다. 브라우저는 근본적으로 화면을 보여주기 위해서 HTML, CSS, JavaScript를 다운로드 받고 그를 처리해서 화면에 픽셀 형태로 그려냅니다. 그리고 이 과정을 CRP(Critical Rendering Path)라고 부릅니다.

Critical Rendering Path는 기본적으로 아래의 과정을 수행합니다.

1. HTML을 파싱해서 DOM을 만든다.
2. CSS를 파싱해서 CSSOM을 만든다.
3. DOM과 CSSOM을 결합해서 Render Tree를 만든다.
4. Render Tree와 Viewport의 width를 통해서 각 요소들의 위치와 크기를 계산한다.**(Layout)**
5. 지금까지 계산된 정보를 이용해 Render Tree상의 요소들을 실제 Pixel로 그려낸다. **(Paint)**

### Reconciliation(재조정)

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

\=> 실제 react 페이지에서 제안하고 있는 비유

1. 업데이트가 발생할 때 기존의 tree와 차이점을 비교하는 방법
2. <mark style="background-color:orange;">DFS로 tree로 Traverse</mark>



#### Render Phase

컴포넌트를 렌더링하고 변경 사항을 계산하는 모든 과정이 이루어지는 단계(`VirtualDOM 조작 단계`)

![](<../../.gitbook/assets/image (14).png>)



<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>



#### Commit Phase

Virtual DOM의 변경점들을 실제 브라우저 DOM에 적용을 시킨다.

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>



**렌더링과 DOM을 업데이트하는 것은 같은 것이 아니며** 컴포넌트는 가시적인 변화가 없어도 렌더링될 수 있습니다.





