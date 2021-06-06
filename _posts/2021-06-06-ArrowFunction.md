```javascript
// 화살표 함수에는 없는 것 : 함수이름, this, arguments 

const myfun = function(){

}
const myFun = () => {
  
}

var myObj = {
  count : 3,
  setCounter : function(){
    console.log(this.count); 
  }
}; 
myBotj.stOcunter(); 
```

 

this가 없기 때문에 this binding 사용 불가. 

호출하는 방법에 의 해 결정됨 

Spread syntax

