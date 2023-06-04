# React Testing Library

> [React Testing Library](https://github.com/testing-library/react-testing-library)

> [jest-dom](https://github.com/testing-library/jest-dom)

로컬 환경(개발환경) node 에서 document를 사용할 수 있는 등.&#x20;

React 환경에 맞게 최대한 사용자 입장에 가깝게 테스트를 할 수 있게 도와준다.



```typescript
import { render, screen } from '@testing-library/react';

import TextField from './TextField';

test('TextField', () => {	
	const text = 'Tester';
	const setText = () => {
		// do nothing...
	};

	render((	
		<TextField
			label="Name"
			placeholder="Input your name"
			text={text}
			setText={setText}		
		/>
	));
	
	screen.getByLabelText('Name');
});
```

테스트 코드, 즉 컴포넌트를 사용하는 코드를 작성하면서 해당 컴포넌트의 인터페이스를 점검할 수 있다.&#x20;

<mark style="background-color:orange;">=> '컴포넌트의 인터페이스'??</mark>

기존에는 label이 빠져있었고, text 같이 범용적인 표현을 사용하지 않은 문제가 있었다. 개발하면서 이런 문제를 발견할 수도 있지만, 우리가 테스트부터 작성했거나 빠르게 테스트 코드를 작성했다면 작성하기 전 또는 바로 직후에 문제를 발견해서 수정할 수 있었을 것.&#x20;

\=> 강의 내용을 보면 기존에 label이 정적으로 'Search'라고 들어가 있었음.

\=> 이 경우를 test 하면 input 의 label 값과 결과의 screen.getLabelText(output)로 유기적으로 연결되어야하는데 그러지 못한 설계의 오류라고 할 수 있어 수정해줌.

\=> 기존에 변수명이filterText라고 되어 있었다.

<mark style="background-color:orange;">=> 여기서 질문이 filterText < text 인가 ??</mark>

시간이 지나면 해당 코드에 대한 지식이 감소하고, 자신감 또한 감소하기 때문에 건드리기 힘든 코드가 되기 십상이다.

\=> 이럴 경우 테스트를 믿고 코드 리펙토링을 시간이 지난 후에도 할 수 있다.

\=> 이 논리는 다른 사람이 설계한 코드를 리펙토링할때도 적용이 된다.



BDD 스타일로 코드를 바꾸고, 입력 등이 잘 작동하는지 확인해보자.

```typescript
import { render, screen, fireEvent } from '@testing-library/react';

import TextField from './TextField';

const context = describe;

describe('TextField', () => {
	const text = 'Tester';
	const setText = jest.fn();
	// let called = false;
	// 안에 명시적으로 작동을 써줘도 됨.
	// const setText = jest.fn(() => {
	//  called = true;
	// }
	
	// setText를 여기저기서 쓰기 때문에 사용할때마다 초기화를 해줘야함
	beforeEach(() => {
		setText.mockClear();
		// 또는 jest.clearAllMocks();	
	});
	
	function renderTextField() {
		render((
			<TextField
				label="Name"
				placeholder="Input your name"
				text={text}
				setText={setText}
			/>
		));
	}
	
	it('renders an input control', () => {
		renderTextField();

		screen.getByLabelText('Name');
	});
	
	context('when user types text', () => {	
		it('calls the change handler', () => {
			renderTextField();
			
			// 이벤트를 생성해줄 수 있음.
			// const input = screen.getByLabelText('Name');
			// input dom에 value를 넣어준것.
			// target, value 형식은 단순 암기
			fireEvent.change(screen.getByLabelText('Name'), {
				target: {
					value: 'New Name',
				},
			});
			
			//then			
			// expect(setText).toBeCalledWith();
			expect(setText).toBeCalledWith('New Name');
		});
	});
});
```

### useCustomHook mock

```typescript
import { render, screen } from '@testing-library/react';

import App from './App';

// 함수안에 함수를 넣어주었다
jest.mock('./hooks/useFetchRestaurants', () => () => [
    {
      id: '1',
      category: '중식',
      name: '메가반점',
      menu: [
        { id: '1', name: '짜장면', price: 8000 },
      ],
    },
  ]
)

describe('App ', () => {
  it('renders without crash', () => {
    render(<App />);

    screen.getByText('메가반점');
  });
});
```

\=> 이런 backend랑 소통하는게 상당히 많고 중요하다.

\=> 그런데 이 부분들의 테스트는 api 에 굉장히 의존적이다.

\=> 그래서  jest mocking 해서 해결.



### fixture 로 데이터 응집

![](<../.gitbook/assets/image (34).png>)

fixtures/restaurants.ts

```typescript
const restaurants = [
  {
    id: '1',
    category: '중식',
    name: '메가반점',
    menu: [
      { id: '1', name: '짜장면', price: 8000 },
    ],
  },
]

export default restaurants;
```

fixtures/index.ts

```typescript
import restaurants from "./restaurants";

export default {restaurants};
```



### hooks \_\_mocks\_\_ 로 함수 로직 응

hooks/\_\_mocks\_\_/useFetchRestaurants.ts

```typescript
import fixtures from "../../fixtures";

const useFetchRestaurants = jest.fn(() => fixtures.restaurants)

export default useFetchRestaurants;
```

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

\=> 그래도 여전히 불편한거 다름 없다 ...

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

\=> 다양한 방법들이 있긴하다 그 중에서 MSW를 우리는 함.



* <mark style="background-color:green;">E2E 테스트와의 차이가 거의 없다고 느껴지기도 함... (실제로 과제 테스트에 쓰인 e2e cypress랑 차이가 없는듯...)</mark>

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

\=> E2E 테스트가 유사하게 느끼고 실제로 유사한게 맞음.

\=> 그러나 E2E 테스트는 실제 유저가 사용하는 시나리오 실제로 우리가 원시적으로 유저시나리오를 짜서 QA를 하는 듯 하는거고

> `React 컴포넌트`를 사용자 입장에 가깝게 테스트할 수 있는 도구

\=> React 컴포넌트를 대상으로 테스트를 하는 것.

\=> 사실 실제로 그 이후의 멘트들은 E2E 테스트와 일치한다.

\=> 그러므로 이 도구는 홀맨님이 언급해주신 것처럼 가볍게 가져간다.

\=> 이걸 통해 React 컴포넌트라는 선이 생기고 컴포넌트 안의 로직들의 테스트에 집중할 수 있게 해줌.



* <mark style="background-color:orange;">어디까지 테스트를 해야할지 시나리오를 짜는 범위에 대한 기준이 없으면 한도 끝도 없이 test 코드가 나올듯...</mark>
* <mark style="background-color:orange;">테스트 코드 짜는 부담 -> 테스트 시나리오에 대한 기획을 해야하는셈이 되는거 아닌가... (업무부담)</mark>

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

> 해당 컴포넌트를 안심하고 믿고 쓸 수 있을 만큼.

*

\=> 이제 제대로 더 배울것임. 추후 내용 추가.

* <mark style="background-color:green;">함수형 프로그래밍과 결합은 의미가 없어지는듯.</mark>









