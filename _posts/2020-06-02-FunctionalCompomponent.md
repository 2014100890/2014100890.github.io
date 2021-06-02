---

layout : single
title : '함수형 컴포넌트의 장점'

---

[참고자료] 함수형 컴포넌트와 클래스, 어떤 차이가 존재할까?

https://overreacted.io/ko/how-are-function-components-different-from-classes



### 일반적인 차이

- 클래스형 컴포넌트의 경우 state 기능 및 라이프 사이클 기능을 사용 (함수형 컴포넌트는 훅스로 해결)
- 함수형 컴포넌트는 메모리 자원을 덜 사용한다, 프로젝트를 완성 후 빌드하고 배포할 때에도 파일 크기가 작다.

**+) 함수형 컴포넌트는 render 될 때의 값들을 유지하지만 클래스 컴포넌트는 유지 하지 않는다.**



### 함수형 컴포넌트 사용 이유

1. 리랜더링 될 때의 값을 유지한다. 즉, immutable 하다.

2. 함수형 컴포넌트는 props에 따른 랜더링 결과를 보장받는다.(immutable한 props를 받기 때문에 결국엔 랜더링 결과가 보장된다는 것. 함수형 프로그래밍의 특징과 일맥상통함이 있음)

3. 매개변수로 받는 props의 destructuring을 활용해 가독성을 보장받을 수 있다.

4. 함수의 모든 장점을 이용할 수 있다.

5. 코드가 간결해지고 가독성도 좋다!

   

------

### 함수형 컴포넌트는 render될 때의 값들을 유지한다.

```tsx
class ProfilePage extends React.Component {
	showMessage = () => {
		alert(`${this.props.user} 를 팔로우 했습니다`);
	}

	handleClick = () => {
		setTimeout(this.showMessage, 5000);
	}

	render() {
		return <button onClick={this.handleClick}>Follow</button>;
	}
}
```

A를 팔로우 한 후, 5초 전에 B유저 프로필로 이동한다면, ⇒ B를 팔로우했습니다  라고 나오게 된다.

this는 mutable하고, 조작할 수 있다.  하지만, props는 immutable 함.

render나 라이프사이클 메서드를 호출할 때 업데이트된 값들을 읽어온다.

요청이 진행되고 있는 상황에서 클래스 컴포넌트가 다시 렌더링 된다면 업데이트 된, this.props 를 받는다.

즉, showMessage 메서드가 “새로운” props의 user를 읽게 된다.



### 클래스형 컴포넌트로 해결해보기

this.props를 조금 더 일찍 부르고, timeout 함수에게는 미리 저장해놓은 값을 전달한다.

But, 여러개의 props에 접근해야 할 때 코드가 비례해서 복잡해짐.

- showMessage가 다른 메서드를 부르고 그 메서드가 this.props.something이나 this.state.something과 같은 코드를 포함해야 한다면 또 다시 문제에 부딪힌다.
- this.props와 this.state를 showMessage가 부르는 모든 메서드에게 일일이 전달 해줘야 한다.

```tsx
class ProfilePage extends React.Component {
	showMessage = (user) => {
		alert(`${this.props.user} 를 팔로우 했습니다`);
	}

	handleClick = () => {
		const {user} = this.props; // 추가 
		setTimeout(this.showMessage(user), 5000);
	}

	render() {
		return <button onClick={this.handleClick}>Follow</button>;
	}
}
```



리액트에서 props와 state는 불변값(immutable)이다.

render에서 props와 state를 클로저로 감싸준다면 우리가 원하는 방식으로 동작할 수 있게 된다.

```tsx
// props값을 Render 될 때의 값으로 고정해두었다. 
class ProfilePage extends React.Component {
	render(){
		//props 값 고정 
		const props = this.props; 
		
		const showMessage = () => {
			alert(`${props.user} 를 팔로우 했습니다`);
		}

		const handleClick = () => {
			setTimeout(showMessage, 5000);
		}

	}
		return <button onClick={handleClick}>Follow</button>;
	}
}
```



매서드들을 render 내부에 선언하는데 굳이 class component 사용? ⇒ functional component 로 작성

```tsx
function ProfilePage(props){
		const showMessage = () => {
			alert(`${props.user} 를 팔로우 했습니다`);
		}

	const handleClick = () => {
			setTimeout(showMessage, 5000);
		}

	return (
     <button onClick={handleClick}>Follow</button>;
  )
}
```



만약, 다른 props를 통해 ProfilePage를 또다시 render되면, 리액트는 ProfilePage를 새로 호출한다.

```jsx
// props destructing을 통한 명확한 표현 

function ProfilePage({user}){
		const showMessage = () => {
			alert(`${user} 를 팔로우 했습니다`);
		}

	const handleClick = () => {
			setTimeout(showMessage, 5000);
		}

	return (
    <button onClick={handleClick}>Follow</button>;
   )
}
```

