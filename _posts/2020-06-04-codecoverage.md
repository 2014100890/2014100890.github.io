---

layout : single
title : '코드 커버리지'

---

[참고자료] 우아한테크코스 : 코드 커버리지가 뭔가요? 

https://woowacourse.github.io/javable/post/2020-10-24-code-coverage/

### 코드커버리지

테스트 수행 결과를 정량적으로 표현하는 방법.

소스 코드 중 테스트를 통해 실행된 비율이다. 화이트 박스 테스트를 통해 측정한다.  

* **테스트 커버리지** : 테스트 대상의 전체 범위에서 테스트를 수행한 범위 

* **블랙 박스 테스트 (Black-box test)**

  * 소프트웨어의 내부 구조나 작동 원리를 모르는 상태에서 동작을 검사하는 방식이다.
  * 올바른 입력과, 올바르지 않은 입력을 입력하여 올바른 출력이 나오는지 테스트 
  * 사용자 관점의 테스트다. 

* **화이트 박스 테스트 (White-box test)**

  * 응용 프로그램의 내부구조와 동작을 검사하는 테스트 방식이다.
  * 소프트웨어 내부 소스코드를 테스트하는 기법이다.
  * 개발자 관점의 단위 테스트 방법이다. 

  

## 측정 기준   

코드의 구조에는 `구문`, `조건`,` 결정`의 구조로 이루어져있다. 



![img](https://mblogthumb-phinf.pstatic.net/MjAxNjEwMjFfMjAz/MDAxNDc3MDQyNzM4OTQy.uRlYllVzUqBOFDf_dakhUI8QHFGYiko_JA_-o5bQFVMg.XlHA7UGMY4M2hPNKe5eW-2IWkuunAd52aYoHUs-xcIog.JPEG.suresofttech/1.png?type=w800)

* 구문(Statement) : 라인 커버리지라고도 부른다. 코드 한 줄이 한 번이라도 실행된다면 충족

  ```c
  void foo(int x){
  	system.out('start line'); // 1번
  	if(x>0){ // 2번 
  		system.out('middle line');// 3번
  	}
  	system.out('last line'); // 4번 
  }
  ```

  x = -1 일 경우, 3번 코드 실행 X 

  구문 커버리지 : (3/4)*100 =75% 

* 조건(Condition) : 모든 조건식의 **내부 조건** 이 true/false을 가지게 되면 충족된다. 

  ```c
  void foo(int x, int y){
  	system.out('start line'); // 1번
  	if(x>0 && y <0){ // 2번 
  		system.out('middle line');// 3번
  	}
  	system.out('last line'); // 4번 
  }
  ```

  * 내부조건 : 조건식 내부의 각각의 조건 ex) x>0, y<0
  * 테스트 케이스 x =1, y=1 과 x = -1, y = -1이 있다. if 문 라인에서 모두 False
  * 조건 커버리지는 만족되었을지 몰라도, 구문 커버리지, 결정 커버리지 만족을 못할 수 있음. 

* 결정(Decision) : 브랜치 커버리지라고 부르기도 한다. 모든 조건식이 true/ false을 가지게 되면 충족. 

  ```c
  void foo(int x, int y){
  	system.out('start line'); // 1번
  	if(x>0 && y <0){ // 2번 
  		system.out('middle line');// 3번
  	}
  	system.out('last line'); // 4번 
  }
  ```

  * 테스트 케이스 x = 1, y = -1 과 x = -1, y =1  이 있다.  모든 조건식에 대해 true와 false를 반환하므로 결정 커버리지를 충족한다. 

* 구문 커버리지가 가장 대표적으로 많이 사용되고 있다. 

  * 조건 커버리지나, 브랜치 커버리지의 경우 로직 시나리오 테스트에 가깝기 때문 

  * 라인 커버리지를 사용하면(만족하면) 모든 시나리오를 테스트한다는 보장은 할 수 없지만, 어떤 코드가 실행되더라도 해당 코드는 문제가 없다는 보장은 할 수 있다

    (True의 경우에만 해보고, False는 안해봤지만,  조건문 내부의 코드가 실행되었을 때 문제는 없군)

  