# 🐶 Week 1 질문 정리

## 📚 JavaScript

### 🎈 const와 var의 차이점은? (실행 컨텍스트 관점에서도 설명하기)
- `var`은 블록 레벨 스코프를 따르지 않기 때문에 코드 내의 변수는 전역 변수로 간주된다.
- `const`와 `let`은 블록 레벨 스코프를 따르기 떄문에 코드 블록 내에 선언된 변수는 지역 변수이다. 따라서 전역에서 변수를 참조할 수 없다.
- `var`은 동일한 이름의 변수는 중복해서 선언할 수 있지만, `let`과 `const`는 동일한 이름으로 변수를 중복해서 선언할 수 없다. (SyntaxError)
- 자바스크립트는 모든 선언을 호이스팅(해당 스코프의 선두로 옮기는 것) 하는데 `let` 키워드는 선언된 변수를 선언문 이전에 참조하면 참조 에러가 발생한다. `let`키워드로 선언된 변수는 스코프의 시작에서 변수의 선언까지 **일시적 사각지대**(**TDZ**)에 빠지기 때문이다.
- 이를 실행 컨텍스트 관점에서 보면 **`var`로 선언된 변수는 선언 단계와 초기화 단계가 한번에 이루어진다.** 즉, 스코프에 변수를 등록하고 메모리에 변수를 위한 공간을 확보한 후, `undefined`로 초기화한다. 때문에 변수 선언문 이전에 변수에 접근하여도 스코프에 변수가 존재하기 떄문에 에러가 발생하지 않고 `undefined`를 반환한다.

```js
console.log(foo); // undefined

var foo;
console.log(foo); // undefined

foo = 1;
console.log(foo); // 1
```
- 하지만, `let` 키워드로 선언된 변수는 선언 단계와 초기화 단계가 분리되어 진행된다. 즉, 스코프에 변수를 등록하지만 **초기화 단계는 변수 선언문에 도달했을 때 이루어진다.** 그렇기 때문에 초기화 이전에 변수에 접근하려고 하니까 참조 에러(ReferenceError)가 발생한다. 다시 말해서 변수를 위한 메모리 공간이 아직 확보되지 않았기 때문에 스코프의 시작 지점부터 초기화 시작 지점까지는 변수를 참조할 수 없게 된다.

```js
// 일시적 사각지대 start
console.log(foo); // ReferenceError: foo is not defined

// 일시적 사각지대 end
let foo; // 변수 선언문에서 초기화 단계가 실행된다.
console.log(foo); // undefined

foo = 1; // 할당문에서 할당 단계가 실행된다.
console.log(foo); // 1
```

- 이 스코프의 시작 지점부터 초기화 시작 지점까지의 구간을 일시적 사각지대라고 부른다.
- `const`는 반드시 선언과 동시에 할당이 이루어져야 한다.
- [📌 참고](https://poiemaweb.com/es6-block-scope)

### 🎈 동기 처리와 비동기 처리의 차이점을 설명해보세요.
- 기본적으로 동기는 **요청 후 응답을 받아야** 다음 동작을 실행하는 방식을 말한다.
- 비동기는 **요청을 보낸 후 응답과 관계없이** 다음 동작을 실행하는 방식을 말한다.
- 자바스크립트는 단일 스레드 프로그래밍 언어이기 때문에 단일 호출 스택이 있어 한 번에 하나의 일을 처리할 수 있다. 그렇기 떄문에 자바스크립트는 동기 방식으로 처리된다. 이때 하나의 호출 스택만 있기 때문에 하나의 함수를 처리하는데 오랜 시간이 걸린다면 다음 실행해야할 함수에 지장을 줄 수 있다.
- 보통 api 통신을 해서 데이터를 서버에서 가져올때와 같은 상황에 많이 사용한다.
- 이 때 이 문제를 해결하는 방법으로 비동기 방식의 처리가 필요하다. 자바스크립트에서 비동기적으로 해결하기 위해서 `callback` 함수를 사용하거나 `promise`, `async await`가 있다.

- [자바스크립트에서 동기와 비동기](https://velog.io/@open_h/javascriptasync)
- [자바스크립트 동기와 비동기](https://pro-self-studier.tistory.com/89)
- [비동기 처리 방식](https://pro-self-studier.tistory.com/10?category=659555)

### 🎈 High Order Function(고차 함수)란 무엇인가?
- 고차 함수란 함수를 인자로 전달받거나 함수를 결과로 반환하는 함수를 말한다.
- 고차 함수는 인자로 받은 함수를 필요한 시점에 호출하거나 클로저를 생성하여 반환한다. 이때 자바스크립트의 함수는 일급 객체이기 때문에 값처럼 인자로 전달할 수 있으며 반환할 수도 있다. 
- 고차 함수는 기본적으로 외부 상태 변경이나 가변 데이터를 피하고 불변성을 지향하는 함수형 프로그래밍에 기반을 두고 있다.
- `Array`의 `map`, `filter`, `reduce`메서드 등이 있다.
- 예제


```js
function makeCounter(predicate) {
  let num = 0;
  // 클로저. num의 상태를 유지한다.
  return function () {
    num = predicate(num);

    return num;
  };
}

function increase(num) {
  return num += 1;
}

function decrease(num) {
  return num -= 1;
}

// 함수를 인자로 받고, 클로저를 반환한다.
const increaser = makeCounter(increase);
increaser(); // 1
increaser(); // 2

const decreaser = makeCounter(decrease);
decreaser(); // -1
decreaser(); // -2
```

- [📌 참고](https://poiemaweb.com/js-array-higher-order-function)

## 📚 Web
### 🎈 웹 브라우저 url에 www.naver.com 를 입력했을 때, 화면이 나오기까지 일어나는 일을 설명해라.

### 🎈 프레임워크와 라이브러리의 차이점
- 프레임워크는 말그대로 뼈대나 기반구조를 뜻하고 라이브러리는 도구들의 집합으로써 둘의 차이점은 **제어 흐름에 대한 주도성이 누구에게/어디에** 있는가에 있다. 즉, 애플리케이션의 흐름을 누가 쥐고 있느냐에 달려 있다.
- 프레임워크는 전체적인 흐름을 스스로가 쥐고 있으며 사용자는 그 안에서 필요한 코드를 짜 넣는다. (가져다 사용한다기보다 거기에 들어가서 사용한다는 느낌)
- 라이브러리는 사용자가 전체적인 흐름을 만들며 라이브러리를 가져다 쓰는 것.
- 즉, 프레임워크는 애플리케이션의 코드는 짜놓은 틀에서 수동적으로 동작해야 하며(제어의 역전), 라이브러리를 사용하는 애플리케이션 코드는 애플리케이션 흐름을 직접 제어한다.
- 간단하게 정리하면 라이브러리는 함수들이나 기능 모음을 가져다가 쓰는 것이고, 프레임워크느는 특정 디자인 패턴이나, 전처리 후처리에 필요한 동작과 기능들을 수행하기 위해서 프레임워크가 실행되다가 중간 중간에 특정 비지니스나, 특정 구현 단에서만 사용자의 코드를 lookup(검색)하여 사용하는 형태이다.

> **👉 예**
> - 라이브러리는 톱, 망치, 삽같은 연장이다. 즉, 사람이 톱을 썰다가, 망치로 바꿔서 내려칠 수도 있고, 삽으로 땅을 팔 수도 있다. 도구를 **선택하는 입장**이기 떄문에 어떤 도구를 사용하든 원하는 것을 만들어낼 수만 있으면 된다.
> - 프레임워크는 차, 비행기 배같은 탈 것이라고 할 수 있다. 탈 것은 정해진 곳으로만 다녀야 한다. 즉, 차를 타고 하늘을 날거나, 배를 타고 땅으로 갈 수는 없다. 하지만, 그 **목적에 맞게** 만들어져 있기 때문에, 톱이나 망치를 들고 탈 것을 만들어야 할 필요가 없다. 그저 정해진 규칙에 맞춰서 엔진, 기어, 핸들만 잘 돌리면 된다.

- [📌 참고](https://webclub.tistory.com/458)

### 🎈 크로스 브라우징 이슈에 대응하는 방법을 설명해주세요.

- [📌 참고](https://asfirstalways.tistory.com/237)


## 📚 React
### 🎈 useCallback은 언제 사용하는가?
- `useCallback`은 주로 렌더링 성능을 최적화해야 하는 상황에서 사용한다. 
- 이 Hook을 사용하면 이벤트 핸들러 함수를 필요할 때만 생성할 수 있다.
- 컴포넌트가 리렌더링될 때마다 함수들도 다시 새롭게 생성된다. 대부분의 경우 이러한 방식은 문제없지만, 컴포넌트의 렌더링이 자주 발생하거나 렌더링해야 할 컴포넌트의 개수가 많아지면 최적화해 주는 것이 좋다. 이때 `useCallback`을 사용하여 최적화할 수 있다.
- `useCallback`은 메모이제이션된 콜백을 반환한다. 첫 번째 파라미터에는 생성하고 싶은 함수를 넣고, 두 번째 파라미터에는 배열을 넣으면 되는데 이때 이 배열에 어떤 값이 바뀌었을 때 함수를 새로 생성해야 하는지 명시해줌으로써 명시된 값이 변경됐을때만 함수가 생성되게 할 수 있다.

### 🎈 클래스형 컴포넌트와 함수형 컴포넌트의 차이는 무엇인가?
- react에서 컴포넌트 선언하는 방법은 두가지로 그 두가지가 클래스형과 함수형 컴포넌트이다.
- 일반적인 차이로는 클래스형은 `state`와 `lifeCycle` 관련 기능을 사용할 수 있다. 하지만 `state`와 `lifeCycle`를 사용하기 떄문에 메모리 자원을 함수형 컴포넌트 대비 상대적으로 많이 사용한다. 
- 이에 반해, 함수형 컴포넌트는 `state`와 `lifeCycle` 관련 기능은 사용할 수 없다. 이 부분에 있어서는 `Hooks`을 사용하여 함수형 컴포넌트에서도 `lifeCycle`과 `state`를 사용할 수 있게 해준다. `Hooks`를 사용함으로 인해서 클래스 컴포넌트의 재사용이 힘든 점을 보안할 수 있다.

- [📌 참고](https://ryublock.tistory.com/55)
- [함수형과 클래스형 차이](https://velog.io/@sdc337dc/0.%ED%81%B4%EB%9E%98%EC%8A%A4%ED%98%95-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8)

### 🎈 JSX란?
- JavaScript 확장 문법으로 JSX는 중괄호에 모든 유효한 JavaScript 표현식을 넣을 수도 있고, JSX 조차도 표현식이다.
- Babel의 컴파일 과정이 끝나면 JSX 표현식이 JavaScript 함수 호출이 되고 JavaScript 객체로 인식된다. 즉, JSX를 `if` 구문 및 `for` loop 안에 사용하고, 변수에 할당하고, 인자로서 받아들이고, 함수로부터 반환할 수 있다.

```jsx
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}

// Babel은 JSX를 React.createElement 호출로 컴파일한다.
function getGreeting(user) {
  if (user) {
    return /*#__PURE__*/_react.default.createElement("h1", null, "Hello, ", formatName(user), "!");
  }

  return /*#__PURE__*/_react.default.createElement("h1", null, "Hello, Stranger.");
}
```

- React는 별도의 파일에 마크업과 로직을 넣어 기술을 인위적으로 분리하는 대신, 둘 다를 포함하는 컴포넌트라고 부르는 느슨하게 연결된 유닛으로 관심사를 분리한다. 이를 위해 사용하는 것이 JS에 마크업을 넣을 수 있게 해주는 JSX문법이다.

- [📌 참고](https://ko.reactjs.org/docs/introducing-jsx.html) 