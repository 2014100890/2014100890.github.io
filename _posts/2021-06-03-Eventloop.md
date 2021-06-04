---

layout : single
title : '이벤트 루프'

---

![Eventloop](https://user-images.githubusercontent.com/31299657/120758179-79685880-c54c-11eb-800c-be7d9e75dd4f.png)

### 자바스크립트 엔진

- 메모리 힙 : 메모리 할당이 일어나는 곳

  - 힙 : 변수, 함수 등이 담김

- 콜 스택 : 실행될 코드가 한 줄 단위로 할당된다.

  (자바스크립트는 인터프리터 언어)

### Web APIs

비동기 처리를 담당한다.

- 자바스크립트 언어 자체가 비동기 동작을 지원하는 것이 아니라, 브라우저가 비동기로 동작하게끔 한다.
- Call Stack에서 실행한 비동기 함수는 Web API를 호출하게 된다.
- Web API는 콜백함수를 Callback Queue에 밀어 넣는다.

### Callback Queue

비동기 처리가 끝난 후 실행되어야 할 콜백함수가 차례로 할당한다.

### Event Loop

Callback Queue에 할당된 함수를 순서에 맞춰 Call Stack에 할당해준다.

Call Stack이 빈 상태가 되면, 첫번째 콜백을 Call Stack으로 밀어넣어준다. 이러한 반복적인 행동을 틱이라 한다.

Call Stack 내에서 현재 실행중인 task가 있는지 검사하고, Callback Queue에도 taskr 있는지 반복해서 검사한다. 만약 Call Stack이 비어있다면 Call back Queue 내의 task를 Call Stack으로 할당시켜줍니다.

⇒ Event Loop와 Queue는 자바스크립트 엔진이 하나의 코드 조각을 하나씩 처리할 수 있도록 스케줄하고, 비동기 작업을 실행하게 해준다.

```jsx
function first(){
	second();
	console.log("첫 번째");
}
function second(){
	third();
  console.log("두 번째");
}
function third(){
  console.log("세 번째");
}
first();
third();
```

실행순서 : 세 번째 → 두번째 → 첫번째 → 세번째

콜스택 : annonymous | first | second | third

```jsx
console.log('시작')

setTimeout(function () {
	console.log('중간')
}, 3000)

console.log("끝")
```

실행순서 : 시작 → 끝 → 중간

![IMG_EC9487203917-1](https://user-images.githubusercontent.com/31299657/120757576-aec07680-c54b-11eb-9bac-2499b9deb6f0.jpeg)

```jsx
// setTimeout 0일때 
console.log('시작')

setTimeout(function () {
	console.log('중간')
}, 0)

console.log("끝")
```

실행순서 : 시작 → 끝 → 중간

```jsx
console.log('시작'); 

setTimeout(function () {
	console.log("중간")
}, 0); 

Promise.resolve().then(function () {
		console.log("프로미스")
	}
)

console.log("끝")
```

실행순서 : 시작 → 끝 → 프로미스 → 중간

Promise는 동기이지만 .then 으로 비동기로 동작하게 됨.

![CallbackQueue](https://user-images.githubusercontent.com/31299657/120758117-69507900-c54c-11eb-879b-9d5fbae189e2.png)

### 우선순위 : Microtask Queue > Animation Frames > Task Queue

- Task Queue : setTimeout이 담김
- MicroTask Queue : Promise 담김

```jsx
console.log('시작')

setTimeout(function () {
	console.log('중간')
}, 0);

Promise.resolve()
	.then(function () {
    console.log('프로미스')
  }
)

requestAnimationFrame(function () {
	console.log('requestAnimationFrame')
})

console.log('끝')
```

실행순서 : 시작 -> 끝 -> 프로미스 -> requestAnimationFrame -> 중간