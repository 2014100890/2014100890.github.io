---

layout : single
title : 'JS 프로처럼 사용하기 '

---

## Ternary Operator (삼항연산자)

### Before

```javascript
function getResult(score) {
  let result;
  if (score > 5) {
    result = '👍';
  } else if (score <= 5) {
    result = '👎';
  }
  return result;
}
```

### After

```javascript
function getResult(score) {
  return score > 5 ? '👍' : '👎';
}
```



## Nullish coalescing operator (널 병합 연산자)

> **leftExpr ?? rightExpr** 

왼쪽이 null 혹은 undefined 일 때 오른쪽 실행됨. 



### Before

```javascript
// ❌ Bad Code 💩
function printMessage(text) {
  let message = text;
  if (text == null || text == undefined) {
    message = 'Nothing to display 😜';
  }
  console.log(message);
}
```

### After

undefined, null 모두 처리 가능 

```javascript
function printMessage(text) {
  const message = text ?? 'Nothing to display 😜';
  console.log(text);
}
```



**Default parameter**

Default parameter is only for undefiend. 

default parameter 사용 시, null 처리 불가 

```javascript
function printMessage(text = 'Nothing to display 😜';) {
  console.log(text);
}

printMessage(undefined) // nothing to display
printMessage(null) // null
```



**Logical OR operator** 

>  leftExpr || rightExpr

왼쪽이 `falsy`인 경우, 오른쪽 실행됨 



**falsy**

false, 0, undefined, null, -0, NaN, '', ``, "" 모두 포함 됨.



value 대신 코드 실행 결과로도 이용 가능하다. 

```javascript
const result = getInitialState() ?? fetchFromServer();
console.log(result);

function getInitialState() {
  return null;
}
function fetchFromServer() {
  return 'Hiya from 💻';
}
```

 

## Object Destructuring

```javascript
const person = {
  name: 'Julia',
  age: 20,
  phone: '0107777777',
};

// ❌ Bad Code 💩
function displayPerson(person) {
  displayAvatar(person.name);
  displayName(person.name);
  displayProfile(person.name, person.age);
}

// ❌ Bad Code 💩
function displayPerson(person) {
  const name = person.name;
  const age = person.age;
  displayAvatar(name);
  displayName(name);
  displayProfile(name, age);
}
```

### Good Code

```javascript
function displayPerson(person){
  const {name, age} = person
  displayAvatar(name);
  displayName(name);
  displayProfile(name, age);
}
```

## Spread Syntax

### Object

기존 오브젝트 값 수정은 바람직 하지 않다. 

```javascript
// Spread Syntax - Object
const item = { type: '👔', size: 'M' };
const detail = { price: 20, made: 'Korea', gender: 'M' };

// ❌ Bad Code 💩
item['price'] = detail.price;

// ❌ Bad Code 💩
const newObject = new Object();
newObject['type'] = item.type;
newObject['size'] = item.size;
newObject['price'] = detail.price;
newObject['made'] = detail.made;
newObject['gender'] = detail.gender;
console.log(newObject);

// ❌ Bad Code 💩
const newObject2 = {
  type: item.type,
  size: item.size,
  price: detail.price,
  made: detail.made,
  gender: detail.gender,
};
console.log(newObject);
```



**Good code** 

Object assign 활용

```javascript
// ✅ Good Code ✨
const shirt0 = Object.assign(item, detail);
console.log(shirt0);

// ✅ Better! Code ✨
const shirt = { ...item, ...detail, price: 30 };
console.log(shirt);
```



### Array

```javascript
// Spread Syntax - Array
let fruits = ['🍉', '🍊', '🍌'];

// 새 과일 추가 방법
// push 사용
// fruits.push('🍓');
fruits = [...fruits, '🍓'];
console.log(fruits);

// 배열 제일 앞에 추가 
// fruits.unshift('🍇');
fruits = ['🍇', ...fruits];
console.log(fruits);

const fruits2 = ['🍈', '🍑', '🍍'];
let combined = fruits.concat(fruits2);
combined = [...fruits, '🍒', ...fruits2];
console.log(combined);
```



## Optional Chaining ?

```javascript
// Optional Chaining
const bob = {
  name: 'Julia',
  age: 20,
};
const anna = {
  name: 'Julia',
  age: 20,
  job: {
    title: 'Software Engineer',
  },
};

// ❌ Bad Code 💩
function displayJobTitle(person) {
  if (person.job && person.job.title) {
    console.log(person.job.title);
  }
}

// job이 있다면 title 검사
// ✅ Good Code ✨
function displayJobTitle(person) {
  if (person.job?.title) {
    console.log(person.job.title);
  }
}

// nullish coalesing 활용
// ✅ Good Code ✨
function displayJobTitle(person) {
  const title = person.job?.title ?? 'No Job Yet 🔥';
  console.log(title);
}

displayJobTitle(bob);
displayJobTitle(anna);
```



## Template Literals (Template String)

```javascript
const person = {
  name: 'Julia',
  score: 4,
};

// ❌ Bad Code 💩
console.log(
  'Hello ' + person.name + ', Your current score is: ' + person.score
);

// ✅ Good Code ✨
console.log(`Hello ${person.name}, Your current score is: ${person.score}`);

// ✅ Good Code ✨
const { name, score } = person;
console.log(`Hello ${name}, Your current score is: ${score}`);

// ✅ Good Code ✨
function greetings(person) {
  const { name, score } = person;
  console.log(`Hello ${name}, Your current score is: ${score}`);
}
```



## Loops

``` javascript
const items = [1,2,3,4,5,6]


// ❌ Bad Code 💩
function getAllEvens(items) {
  const result = [];
  for (let i = 0; i < items.length; i++) {
    if (items[i] % 2 === 0) {
      result.push(items[i]);
    }
  }
  return result;
}

function multiplyByFour(items) {
  const result = [];
  for (let i = 0; i < items.length; i++) {
    result.push(items[i] * 4);
  }
  return result;
}

function sumArray(items) {
  let sum = 0;
  for (let i = 0; i < items.length; i++) {
    sum += items[i];
  }
  return sum;
}

const evens = getAllEvens(items);
const multiple = multiplyByFour(evens);
const sum = sumArray(multiple);
console.log(sum);

// ✅ Good Code ✨
const evens = items.filter((num) => num % 2 === 0);
const multiple = evens.map((num) => num * 4);
const sum = multiple.reduce((a, b) => a + b, 0);
console.log(sum);

// ✅ Good Code ✨
const result = items
  .filter((num) => num % 2 === 0)
  .map((num) => num * 4)
  .reduce((a, b) => a + b, 0);
console.log(result);
```



## Async, Await 

```javascript
// Promise -> Async/await

// ❌ Bad Code 💩
function displayUser() {
  fetchUser() //
    .then((user) => {
      fetchProfile(user) //
        .then((profile) => {
          updateUI(user, profile);
        });
    });
}

// ✅ Good Code ✨
async function displayUser() {
  const user = await fetchUser();
  const profile = await fetchProfile(user);
  updateUI(user, profile);
}
```



## Quiz

```javascript
// Remove Duplicates!
const array = ['🐶', '🐱', '🐈', '🐶', '🦮', '🐱'];

console.log(array);

console.log([...new Set(array)]);
```

