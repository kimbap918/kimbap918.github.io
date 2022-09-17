---
layout: post
title: JavaScript(3) - 데이터 타입, 연산자 
date: 2022-09-16 12:05:00 +0900
image: JS.png
tags: JS
categories: JS
---

<br>

## 데이터 타입

* 자바스크립트의 모든 값은 특정한 데이터 타입을 가짐

* 크게 원시 타입(Primitive type)과 참조 타입(Reference type)으로 분류됨

* Primitive type

  * 객체가 아닌 기본 타입
  * 변수에 해당 타입의 값이 담긴다
  * 다른 변수에 복사할 때 실제 값이 복사됨

* Reference type

  * 객체 타입의 자료형
  * 변수에 해당 객체의 참조 값이 담김
  * 다른 변수에 복사할 때 참조 값이 복사됨

* 숫자 타입

  * 정수, 실수 구분 없는 하나의 숫자 타입
  * 부동소수점 형식을 타름
  * Nan(Not-A-Number)
    * 계산 불가능한 경우 반환되는 값

* 문자열(String) 타입

  * 텍스트 데이터를 나타내는 타입

  * 16비트 유니코드 문자의 집합

  * 작은따옴표 또는 큰따옴표 모두 가능

  * 템플릿 리터럴(Templete Literal)

    * ES6부터 지원

    * 따옴표 대신 backtrack(`)으로 표현

    * ${ expression } 형태로 표현식 삽입 가능

      ``` javascript
      const firstName = 'Brandan'
      const lastName = 'Eich'
      const fullName = `${firstName} ${lastName}`
      
      console.log(fullName) // Brandan Eich
      ```

* undefined

  * 변수의 값이 없음을 나타내는 데이터 타입

  * 변수 선언 이후 직접 값을 할당하지 않으면, 자동으로 undefined가 할당됨

    ``` javascript
    let firstName
    console.log(firstName) // undefined
    ```

* null

  * 변수의 값이 없음을 의도적으로 표현할 때 사용하는 데이터 타입

  * typeof : 자료형 평가를 위해 사용하는 연산자 

  * null의 typeof 연산자의 결과는 ECMA 명세의 원시 타입 정의에 따르면 원시 타입에 속하지만 객체(object)로 표현됨

    ``` javascript
    let firstName = null
    console.log(firstName) // null
    
    typeof null // object
    ```

* Boolean 타입

  * 논리적 참 또는 거짓을 나타내는 타입

  * true 또는 false로 표현

  * 조건문 또는 반복문에서 유용하게 사용

    ``` javascript
    let isAdmin = true
    console.log(isAdmin) // true
    
    isAdmin = false
    console.log(isAdmin) // false
    ```

<br>

## 연산자

* 할당 연산자

  * 오른쪽에 있는 피연산자의 평가 결과를 왼쪽 피연산자에 할당하는 연산자

  * 다양한 연산에 대한 단축 연산자 지원

  * ++ 및 -- 연산자

    * ++ : 피연산자의 값을 1 증가시키는 연산자

    * -- : 피연산자의 값을 1 감소시키는 연산자 

      ``` javascript
      let x = 0
      
      x += 10
      x -= 3
      x *= 10
      x /= 10
      x++
      x-- 
      ```

* 비교 연산자

  * 피연산자를 비교하고 결과값을 boolean으로 반환하는 연산자

  * 문자열은 유니코드의 값을 사용하며 표준 사전 순서를 기반으로 비교

    ``` javascript
    const numOne = 1
    const numTwo = 100
    console.log(numOne < numTwo) // True
    
    const charOne = 'a'
    const charTwo = 'z'
    console.log(charOne > charTwo) // false
    ```

* 동등 비교 연산자(==)

  * 두 피연산자가 같은 값으로 평가되는지 비교 후 boolean 값을 반환

  * 비교할때 암묵적 타입 변환을 통해 타입을 일치시킨 후 같은 값인지 비교

  * 두 피연산자가 모두 객체일 경우 메모리의 같은 객체를 바라보는지 판별

  * 예상치 못한 결과가 발생할 수 있으므로 특별한 경우를 제외하고 사용하지 않는다

    ``` javascript
    const a = 1004
    const b = '1004'
    console.log(a == b) // true
    
    const c = 1
    const d = true
    console.log(c == d) // true
    ```

* 일치 비교 연산자(===)

  * 두 피연산자가 같은 값으로 평가되는지 비교 후 boolean 값을 반환

  * 엄격한 비교가 이뤄지며 암묵적 타입 변환이 발생하지 않음

    * 엄격한 비교 : 두 비교 대상의 타입과 값 모두 같은지 비교

      ``` javascript
      const a = 1004
      const b = '1004'
      console.log(a === b) // false
      ```

* 논리 연산자

  * 세 가지 논리 연산자로 구성

  * and 연산은 && 연산자 이용

  * or 연산은 || 연산자 이용

  * not 연산은 ! 연산자를 이용

    ``` javascript
    console.log(true && false) // false
    console.log(1 && 0) // 0
    console.log(true || false) // ture
    console.log(1 || 0) // 1
    console.log(!true) // false
    ```

* 삼항 연산자

  * 세 개의 피연산자를 사용해 조건에 따라 값을 반환하는 연산자

  * 가장 왼쪽의 조건식이 참이면 : 앞의 값을 사용하고 그렇지 않으면 뒤의 값 사용

    ``` javascript
    console.log(true ? 1 : 2) // 1
    ```

    
