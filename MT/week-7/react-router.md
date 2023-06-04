# React Router

### Routing

결국 React Router Dom 도 if 문으로 컴포넌트를 분리해준 것이다.

window.location 내장함수들을 사용해서.



### React Router Dom 라이브러리

React Router Dom에서 제공하는

Routes, Route 컴포넌트들이 컴포넌트들을 분리해줌

BrowserRouter 가 contextAPI를 이용해서 App에 라우팅 이용



### 테스트 코드에선 MemoryRouter  사용

실제 코드에서 BrowserRouter > App이 한 세트인 것 처럼

테스트 코드에서도 MemoryRouter > App이 한 세트.

> [MemoryRouter](https://reactrouter.com/en/main/router-components/memory-router)

```tsx
describe('App', () => {
	function renderApp(path: string) {
		render((
			<MemoryRouter initialEntries={[path]}>
				<App />
			</MemoryRouter>
		));
	}
	
	context('when the current path is “/”', () => {
		it('renders the home page', () => {
			renderApp('/');

			screen.getByText(/Hello/);
		});
	});
	
	context('when the current path is “/about”', () => {
		it('renders the about page', () => {
			renderApp('/about');

			screen.getByText(/About/);
		});
	});
});
```



* \<Router> : Route, Link 컴포넌트를 연결시켜주는 컴포넌트이다. Router 컴포넌트를 상위 컴포넌트로 가져야 한다.
  * \<BrowserRouter> : HTML5의 history API를 활용한 라우터이다. 주로 사용된다.
  * \<HashRouter> : 주소창에 #(Hash)가 붙는다. 검색 엔진이 읽지 못한다. 거의 사용되지 않음.
* \<Route> : URL 경로와 연결된 컴포넌트를 보여준다. props로 path(매치 경로)와 component(보여줄 컴포넌트)를 받는다.&#x20;
* \<Link> : \<a> 태그와 역할이 동일하다. 새로고침이 되지 않는다는 것이 차이점이다.  props로 to(이동할 경로)를 받는다.&#x20;

\




