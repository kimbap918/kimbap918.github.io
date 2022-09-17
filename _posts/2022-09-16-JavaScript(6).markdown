---
layout: post
title: JavaScript(6) - 함수, 배열, 객체
date: 2022-09-16 12:20:00 +0900
image: JS.png
tags: JS
categories: JS
---

<br>

## 함수

* 참조 타입 중 하나로, function 타입에 속함
* JS에서 함수를 정의하는 방법은 주로 2가지
  * 함수 선언식
  * 함수 표현식
* JS의 함수는 일급 객체에 해당
  * 일급 객체 : 다음의 조건들을 만족하는 객체를 의미함
    * 변수에 할당 가능
    * 함수의 매개변수로 전달 가능
    * 함수의 반환 값으로 사용 가능

<br>

#### 함수의 정의

* 함수의 이름과 함께 정의하는 방식

* 3가지 부분으로 구성

  * 함수의 이름 (name)

  * 매개변수 (args)

  * 함수 body (중괄호 내부)

    ``` javascript
    function add(num1, num2) {
      return num1 + num2
    }
    
    add(1, 2)
    ```

* 함수 표현식

  * 함수를 표현식 내에서 정의하는 방식

    * 표현식 : 어떤 하나의 값으로 결정되는 코드의 단위

  * 함수의 이름을 생략하고 익명 함수로 정의 가능

    * 익명 함수 : 이름이 없는 함수
    * 익명 함수는 함수 표현식에서만 가능

  * 3가지 부분으로 구성

    * 함수의 이름 (생략 가능)

    * 매개변수 (args)

    * body (중괄호 내부)

      ``` javascript
      const add = function (num1, num2) {
        return num1 + num2
      }
      
      add(num1, num2)
      ```

* 기본 인자 : 인자 작성 시 '=' 문자 뒤 기본 인자 선언 가능  

  ``` javascript
  const add = function (num1 = 1, num2 = 2) {
    return num1 + num2
  }
  ```

* **매개변수와 인자의 개수 불일치 허용**

  * 매개변수보다 인자의 개수가 많을 경우

    ``` javascript
    const noArgs = funstion () {
      return 0
    }
    
    noArgs(1, 2, 3) // 0
    
    const twoArgs = function (arg1, arg2) {
      return [arg1, arg2]
    }
    
    twoArgs(1, 2, 3) // [1, 2]
    ```

  * 매개변수보다 인자의 개수가 적을 경우

    ``` javascript
    const twoArgs = function (arg1, arg2) {
      return [arg1, arg2]
    }
    
    twoArgs() // [undefined, undefined]
    ```

* Rest Parameter

  * rest parameter(...)을 사용하면 함수가  정해지지 않은 수의 매개변수를 열로 받음

    ``` javascript
    const restOpr = function(arg1, arg2, ...restArgs) {
      return [arg1, arg2, restargs]
    }
    
    restargs(1, 2, 3, 4, 5) // [1, 2, [3, 4, 5]]
    ```

* Spread operator

  * spread operator(...)를 사용하면 배열 인자를 전개하여 전개 가능

    ``` javascript
    const spreadOpr = function(arg1, arg2, arg3) {
      return arg1 + arg2 + arg3
    }
    
    const numbers = [1, 2, 3]
    spreadOpr(...numbers) // 6
    ```

<br>

#### 선언식 vs 표현식

함수의 타입

* 선언식의 함수와 표현식의 함수 모두 타입은 function으로 동일

  ``` javascript
  // 함수 표현식
  const add = function (args) {}
  
  // 함수 선언식
  function sub(args) {}
  
  console.log(typeof add) // function
  console.log(typeof sub) // function
  ```

호이스팅

* 함수 표현식

  * 함수 표현식으로 선언한 함수는 함수 정의 전에 호출 시 에러 발생

  * 함수 표현식으로 정의된 함수는 변수로 평가되어 scope규칙을 따름

    ``` javascript
    sub(7, 2) // 에러
    
    const sub = function (num1, num2) {
      return num1 - num2
    }
    ```

<br>

#### 화살표 함수(Arrow Function)

* 함수를 비교적 간결하게 정의할 수 있는 문법

* function 키워드 생략 가능

* 함수의 매개변수가 단 하나뿐이라면, () 도 생략 가능

* 함수의 body가 표현식 하나라면 {} 과 return도 생략 가능

  ``` javascript
  const arrow1 = function (name) {
    return `hello, ${name}`
  }
  // function 키워드 삭제
  const arrow2 = (name) => {return `hello, ${name}`}
  // 매개변수가 1개일 경우에는 () 삭제가능
  const arrow3 = name => {return `hello, ${name}`}
  // 함수의 body가 표현식 하나라면 {} 과 return도 생략 가능
  const arrow4 = name => `hello, ${name}`
  ```

<br>

## 배열

* 키와 속성들을 담고 있는 참조 타입의 객체(objcet)

* 순서를 보장하는 특징이 있다

* 주로 대괄호를 이용하여 생성하고, 0을 포함한 양의 정수 인덱스로 특정 값에 접근 가능

* 배열의 길이는 array.length 형태로 접근 가능

  ``` javascript
  const numbers = [1, 2, 3, 4, 5]
  
  console.log(numbers[numbers.length - 1]) // 5
  ```

<br>

#### 배열 관련 주요 메서드

* array.unshift() : 가장 앞에 요소 추가

* array.shift() : 배열의 첫번째 요소 제거 

* array.includes(value) : 배열의 특정 값이 존재하는지 판별 후 참 또는 거짓 반환

* array.indexOf(value) : 배열에 특정 값이 존재하는지 확인 후 가장 첫번째로 찾은 요소의 인덱스 반환 값이 없을경우 -1 반환 

* array.join([separator]) : 배열의 모든 요소를 연결하여 반환, 구분자는 선택적으로 지정 생략시 쉼표가 기본값

* array.forEach(callback(element[, index[,array]]))

  * 배열의 각 요소에 대해 콜백 함수를 한 번씩 실행

  * 콜백 함수는 3가지 매개변수로 구성

    * element: 배열의 요소
    * index : 배열 요소의 인덱스
    * array : 배열 자체

  * 반환값이 없는 메서드

    ``` javascript
    array.forEach((element, index, array) => {
      // do something
    })
    
    const fruits = ['딸기', '수박', '사과', '체리']
    
    fruits.forEach((fruit, index) => {
      console.log(fruit, index)
      // 딸기 0
      // 수박 1
      // 사과 2
      // 체리 3
    })
    ```

* array.map(callback(element[, index[, array]]))

  * 배열의 각 요소에 대해 콜백 함수를 한번씩 실행

  * 콜백 함수의 반환 값을 요소로 하는 새로운 배열 반환

  * 기존 배열 전체를 다른 형태로 바꿀때 유용

    ``` javascript
    array.map((element, index, array) => {
      // do something
    })
    
    const numbers = [1, 2, 3, 4, 5]
    
    const doubleNums = numbers.map((num) => {
      return num * 2
    })
    
    console.log(doubleNums) // [2, 4, 6, 8, 10]
    ```

* array.reduce(callback(acc, element, [index[, array]])[, initialValue])

  * 배열의 각 요소에 대해 콜백 함수를 한 번씩 실행

  * 콜백 함수의 반환 값들을 하나의 값(acc)에 누적 후 반환

  * reduce 메서드의 주요 매개변수

    * acc
      * 이전 callback 함수의 반환 값이 누적되는 변수
    * initialValue(optional)
    * 최초  callback 함수 호출 시 acc에 할당되는 값, default 값은 배열의 첫 번째 값

    ``` JavaScript
    array.reduce((acc, element, index, array) => {
      // do something
    }, initialValue)
    
    const numbers = [1, 2, 3]
    const result = numbers.reduce((acc, num) => {
      return acc + num
    }, 0)
    
    console.log(result) // 6
    ```

* array.some(callback(element[, index[, array]]))

  * 배열의 요소 중 하나라도 주어진 판별 함수를 통과하면 참을 반환 

* array.every(callback(element[, index[, array]]))

  * 배열의 모든 요소가 주어진 판별 함수를 통과하면 참을 반환 

<br>

## 객체 

객체의 정의와 특징 

* 객체는 속성(propety)의 집합이며, 중괄호 내부에 key와 value의 쌍으로 표현

* key는 문자열 타입만 가능

* value는 모든 타입(함수 포함) 가능

* 객체 요소 접근은 점 또는 대괄호로 가능

  ``` javascript
  const me = {
    name : 'jack',
    phoneNumber : '012345678',
    'samsung products' : {
      buds : 'Galaxy Buds pro',
      galaxy : 'Galaxy s20'
    },
  }
  
  console.log(me.name)
  ```

* 메서드는 객체의 속성이 참조하는 함수

* 객체.메서드명() 으로 호출 가능

* 메서드 내부에서는 this 키워드가 객체 를 의미

  ``` javascript
  const me = {
    firstName: 'John',
    lastName: 'Doe',
    getFullName: function () {
      return this.firstName + this.lastName
    }
  }
  ```

  
