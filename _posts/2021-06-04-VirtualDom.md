---

layout : single
title : 'Virtual DOM'

---

### Virtual DOM

html DOM의 추상화 버전이다. 

변화가 일어나면 실제로 브라우저의 DOM을 변화시키는 것이 아닌, 

Javascript로 이루어진 가상의 DOM에 한 번 랜더링을 하고, 

기존의 DOM과 비교를 한 다음 변화가 필요한 곳에만 업데이트 해준다. 



실제 돔과 같은 속성 ex) class등 은 가지고 있지만, 실제 DOM이 가지고 있는 api는 가지고 있지 않다. 

ex) getElementById, createElement 등 



데티어가 변경되면 전체 UI는 Virtual Dom에 랜더링 된다. 

그리고 이전 VIrtual DOM에 있던 내용과 업데이트 후에 내용을 비교하여 실제 바뀐 부분만 실제 DOM에 적용시킵니다. 



Javascript 객체로 표현

메모리 상에서 동작

실제 렌더 X -> 연산 비용 최소화





DOM Fragment의 변화를 붂어 적용한 다음 기존 DOM에 던져주는 과정 

VirtualDOM 은 이 과정을 자동화, 추상화 해놓은 것에 불과하다.  



UI의 가상적인 표현을 메모리에 저장하고,

ReactDOM과 같은 라이브러리에 의해 실제 DOM과 동기화 : 재조정 



모든 React DOM Object는 그에 대응하는 Virtual DOM object가 있다.

Virtual DOM object는 DOM object를 대신한다. 



### Diffing

virtual DOM이 업데이트 되면, React는 virtual DOM을 업데이트 이전의 virtual DOM 스냅샷과 비교하여, 정확히 어떤 DOM 이 바뀌었는지 검사한다. 



