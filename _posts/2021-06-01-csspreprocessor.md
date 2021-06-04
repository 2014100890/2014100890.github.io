---

layout : single
title : 'CSS 전처리기'

---

### CSS 전처리기, SASS(SCSS)

### Cascading Style Sheets Preprocessor

기본적인 css는, 코드를 중복적으로 적고, 다른 브라우저의 호환성을 위해  반복적으로 해주어야 할 일 등 유지보수에 불편함이 있다. 

CSS 전처리기는 코드의 중복성을 줄여주고, 가독성을 높여주는 도구다. 

Ex) PostCSS, LESS, SASS(SCSS), Stylus

위 프레임워크에 맞게 컴파일 하면 순수 css로 변환해서 브라우저가 이해할 수 있도록 해준다. 



### SCSS

* SASS에 SCSS 포함되어 있음. SASS 3번째 버전에서 추가되었다. 
* SCSS는 SASS의 모든 기능을 지원하면서, **CSS 구문과 완전히 호환**되도록 만들어졌다. 



### 장점

1. Nesting 등의 기능을 통해 코드의 양을 줄이고, 연관된 코드끼리 그룹핑 해서 코드의 중복을 줄인다.
2. 변수 선언 및 @mixin 기능 등을 사용할 수 있기 때문에 유지보수가 쉬워진다. 
3. 조건문, 반복문, 연산자 등을 사용할 수 있다. 



### 단점

1. 전처리기로 작성한 것은 웹에서 작동하지 않기에, css 파일로 컴파일을 하는, 전처리기를 위한 도구가 필요. 컴파일 하는데 시간 + 



```css
// CSS
.wrapper{
  width: 100px;
  height: 200px;
}
.wrapper .content{
  color: white;
  float: left; 
}
```

```scss
// SASS
.wrapper
  width: 100px
  height: 200px
.content
  color: white
  float: left
```



### SASS(SCSS)의 주요기능 

### 1.Nesting(둥지)

부모 선택자 내부에서 자식 선택자를 사용하여, 부모 선택자를 중복적으로 작성하는 것을 방지한다. 

```scss
.wrapper{
  width: 100px;
  height: 200px;
	.content{
  color: white;
  float: left; 
	}
}
```



### 2. & 부모참조연산자 

```scss
 // CSS
 .menu {
 	background: red; 
 }
 .menu:hover{
 	background: green; 
 }
 // SCSS
 .menu {
 	background: red; 
 	&:hover{
 		background: green;
  }
 }
```



### 3. $로 쉬운 변수 선언

```
 // CSS
 :root {
 	--font-color: red; 
 }
 body{
 	color: var(--font-color);
 }
 // SCSS
$font-color: red;
body{
	color: $font-color; 
}
```



### 4. @mixin / @include 

공통적으로 많이 쓰이는 css속성들을 그룹화하여 재사용할 수 있게한다. 

```
 // CSS
 .section{
 	position: relative; 
 }
 .section .box1{
 	width: 100px; 
 	height: 50px; 
 }
 .section .box2{
 	width: 100px; 
 	height: 50px; 
 }
```

```// CSS
 @mixin box-style{
 	width: 100px; 
 	height: 50px; 
 }
 .section {
 	position: relative;
 	.box1{
 		@include box-style;
 	}
 	.box2{
 		@include box-style;
 	}
 }
```

```
@mixin box-style($size1, $size2){
 	width: $size1; 
 	height: $size2; 
 }
 .section {
 	position: relative;
 	.box1{
 		@include box-style(100px, 50px);
 	}
 	.box2{
 		@include box-style(30px, 20px);
 	}
 }
```



### 5. @import

다른 파일을 연결시킬 수 있다. 



```
//style.css
header{
	...
}
section{
  ...
}
aside{
 ...
}
footer{
 ...
}
```

```
@import 'header.scss';
@import 'section' // 확장자 생략 가능 
```



### 6. if문 사용 

```
// if(condition, true, false) 삼항연산자 
$type: box;

article{
	background: if($type == box, blue, green)
}
```



```// if(condition, true, false) 삼항연산자 
// @if 
$type: box;

.article{
	@if $type == box{
		color: blue;
	}
	$else if $type == list{
		color: green;
	}
}
```



### 7. 반복문(for)

```scss
//@for-to 마지막 포함 X
//@for iteration from ~ [to, through]
@for $i from 1 to 3{
	.box-#{$i}{
		width: 2em * $i
	}
}
//CSS compiled
.box-1 {width: 2em;}
.box-2 {width: 4em;}
```

```scss
//@for-through
//@for iteration from ~ [to, through]
@for $i from 1 thorugh 3{
	.box-#{$i}{
		width: 2em * $i
	}
}
//CSS compiled
.box-1 {width: 2em;}
.box-2 {width: 4em;}
.box-3 {width: 4em;}
```



### 8. 반복문(While)

```scss
//@while
$i: 5;
@while $1< 10{
  .box-#{$1}{
    width: 2em * $i;
  }
  $i: $i+2;
}
//CSS compiled
.box-5 {width: 10em;}
.box-7 {width: 14em;}
.box-9 {width: 18em;}
```





