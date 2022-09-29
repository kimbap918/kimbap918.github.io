---
layout: post
title: JavaScript(2) - 변수와 식별자
date: 2022-09-16 12:00:00 +0900
image: JS.png
tags: JS
categories: JS
---

<br>

## ECMA Script

## 코딩 스타일 가이드

* 코딩 스타일의 핵심은 합의된 원칙과 일관성
  * 절대적인 하나의 정답은 없으며, 상황에 맞게 원칙을 정하고 일관성 있게 사용하는 것이 중요하다.
* 코딩 스타일은 코드의 품질에 직결되는 중요한 요소
  * 코드의 가독성, 유지보수 또는 팀원과의 커뮤니케이션 등 개발 과정 전체에 영향을 끼친다.

<br>

## 변수와 식별자

* 식별자는 변수를 구분할 수 있는 변수명을 말한다.
* 식별자는 반드시 문자, 달려($) 또는 밑줄(_)로 시작
* 대소문자를 구분하며, 클래스명 외에는 모두 소문자로 시작된다
* 예약어 사용 불가능 (for, if, function 등)

<br>

#### 선언, 할당, 초기화

* 선언(Declaration)
  * 변수를 생성하는 행위 또는 시점
* 할당(Assignment)
  * 선언된 변수에 값을 저장하는 행위 또는 시점
* 초기화(Initialization)
  * 선언된 변수에 처음으로 값을 저장하는 행위 또는 시점

``` javascript
let foo
console.log(foo)

foo = 11
console.log(foo)

let bar = 0
console.log(bar)
```

<br>

#### let, const

``` javascript
let number = 10 // 1. 선언 및 초기값 할당
number = 10 // 2. 재할당

console.log(number) // 3. 10

let number = 10 // 1. 선언 및 초기값 할당
let number = 50 // 2. 재선언 불가능
```

let(재할당 가능, 재선언 불가능, 블록 스코프)

<br>

``` javascript
const number = 10 // 1. 선언 및 초기값 할당
number = 10 // 2. 재할당 불가능

const number = 10 // 1. 선언 및 초기값 할당
const number = 50 // 2. 재선언 불가능
```

const(재할당 불가능, 재선언 불가능, 블록 스코프)

<br>

* 블록 스코프(block scope)

  * if, for,  함수등의 중괄호 내부를 가리킴

  * 블록 스코프를 가지는 변수는 블록 바깥에서 접근 불가능

    ``` javascript
    let x = 1
    
    if (x === 1) {
      let x = 2
      console.log(x) // 2
    }
    
    console.log(x) // 1
    ```

<br>

#### var

* var로 선언한 변수는 재선언 및 재할당 모두 가능
* ES6 이전에 변수를 선언할 때 사용되던 키워드
* 호이스팅 되는 특성으로 인해 예기치 못한 문제 발생 가능
  * 호이스팅(hoisting)
    * 변수를 선언 이전에 참조할 수 있는 현상
    * 변수 선언 이전의 위치에서 접근 시 undefined를 반환
    * 자바스크립트는 모든 선언을 호이스팅한다.
    * var, let, const 모두 호이스팅이 발생하지만, var는 선언과 초기화가 동시에 발생하여 일시적으로 사각지대가 존재하지 않는다.
* 함수 스코프
  * 함수의 중괄호 내부를 가리킴
  * 함수 스코프를 가지는 변수는 함수 바깥에서 접근 불가능

``` javascript
function foo() {
  var x = 5
  console.log(x)
}
// ReferenceError: x is not defined
console.log(x)
```

