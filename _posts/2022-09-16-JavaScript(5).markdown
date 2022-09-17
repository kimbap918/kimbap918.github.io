---
layout: post
title: JavaScript(5) - 조건문, 반복문 
date: 2022-09-16 12:15:00 +0900
image: JS.png
tags: JS
categories: JS
---

<br>

## 조건문

조건문의 종류와 특징

* if, else if, else

  * 조건은 소괄호() 안에 작성 

  * 실행할 코드는 중괄호{} 안에 작성

  * 블록 스코프 생성 

    ``` javascript
    const nation = 'korea'
    
    if (nation === 'korea') {
      console.log('안녕하세요') 
    } else if (nation === 'France') {
      console.log('Bonjour')
    } else {
      console.log('Hello!')
    }
    ```

* switch

  * 표현식의 결과값과 case문의 오른쪽 값을 비교

  * break 및 default문은 [선택적]으로 사용 가능

  * break문을 만나거나 default문을 실행할 때까지 다음 조건문 실행

    ``` javascript
    const nation = 'korea'
    
    switch(nation) {
      case 'korea': {
        console.log('안녕하세요!')
      }
      case 'France': {
        console.log('Bonjour!')
      }
      default: {
        console.log('Hello!')
      }
    }
    // 이 경우에는 break문이 없으므로 모두 출력
    ```

<br>

## 반복문

반복문의 종류와 특징

* while

  * 조건문이 참(true)일 경우에만 반복 시행

  * 조건은 소괄호 안에 작성

  * 실행할 코드는 중괄호 안에 작성

  * 블록 스코프 생성

    ``` javascript
    while (condition) {
      // do something
    }
    ```

* for

  * 세미콜론(;)으로 구분되는 세 부분으로 구성

  * initialization : 최초 반복문 진입 시 1회만 실행

  * condition : 매 반복 시행 전 평가되는 부분 

  * expression : 매 반복 시행 이후 평가되는 부분

  * 블록 스코프 생성

    ``` javascript
    for (initialization; condition; expression) {
      // do something
    }
    
    for (let i = 0; i < 6; i++) {
      console.log(i) // 0, 1, 2, 3, 4, 5
    }
    ```

* for ... in

  * 객체(object)의 속성(key)들을 순회할 때 사용

  * 배열도 순회 가능하지만 권장되지 않음

  * 실행할 코드는 중괄호 안에 작성

  * 블록 스코프 생성

    ``` javascript
    for (variable in object) {
      // do something
    }
    
    const capitals = {
      korea: 'seoul',
      france: 'paris',
      USA: 'washington D.C.'
    }
    
    for (let capital in capitals) {
      console.log(capital) // korea, france, USA
    }
    ```

* for ...of

  * 반복가능한 객체를 순회하며 값을 꺼낼때 사용

  * 실행할 코드는 중괄호 안에 작성

  * 블록 스코프 생성

    ``` javascript
    for (variable of iterables) {
      /// do something
    }
    
    const fruits = ['딸기', '바나나', '메론']
    
    for (let fruit of fruits) {
      fruit = fruit + '!'
      console.log(fruit)
    }
    ```

<br>
