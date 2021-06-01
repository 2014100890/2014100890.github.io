---

layout : single
title : 'React의 Lifecycle'

---

공부자료 : https://react.vlpt.us/basic/25-lifecycle.html



# LifeCycle  

React의 클래스형 컴포넌트에서 사용하는 LifeCycle API는 컴포넌트가 DOM위에 생성되거나, 업데이트 되거나, 사라질 때 호출되는 API입니다. 



![React LifeCycle API 생명주기](https://media.vlpt.us/images/760kry/post/c309e243-32f6-4b5c-86d4-e1147a4905a2/image.png)



### constructor

`constructor` 는 컴포넌트의 생성자 메소드입니다. 컴포넌트가 만들어지면 가장 먼저 실행됩니다. 



### getDerivedStateFromProps

props로 받아온 것을 state에 넣어주고 싶을 때 사용한다. 

```react
 static getDerivedStateFromProps(nextProps, prevState) {
    console.log("getDerivedStateFromProps");
    if (nextProps.color !== prevState.color) {
      return { color: nextProps.color };
    }
    return null;
  }
```

정적 메서드이기 때문에 this를 호출할 수 없다. 







## 초기 구성 : Mounting

React 컴포넌트 객체가 DOM에 실제로 삽입되기 전까지의 과정

= Component를 브라우저에 나타나는 것 

1. constructor() : 특정 컴포넌트에 대한 초기화 
2. getDerivedStateFromProps()
3. render() : 화면 구성 
4. componentDidMount() : 처리가 끝난 후에 불러짐 

constructor는 초기 상태값을 만든다. this.state로 초기 상태값을 설정한다. 

기본적으로 컴포넌트가 모두 구성된 직후인 componentDidMount() 함수에서 API를 호출하면 효과적이다. 



## 데이터 변경 : Updating

component의 state나 props가 바뀌었을 때 

1. shouldComponentUpdate() : 상태 변화 감지 
2. componentWillUpdate()
3. Render()
4. componenetDidUpdate()

 화면에 출력되는 화면 구성을 변경하고자 할 때는 componentDidUpdate()를 많이 사용한다.



## 컴포넌트 해체 : Unmounting

컴포넌트가 마운팅 해제될 때 수행되는 함수는 componentWillUnmount() 다. 이 함수를 이용해서 컴포넌트의 동작을 위해 사용되었던 메소드들의 리소스를 제거한다. 