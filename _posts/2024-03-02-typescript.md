---
title: TypeScript 와 JavaScript의 차이점
author: happywerrior
date: 2024-03-02 22:15:00 +0900
categories: [Blogging, TypeScript]
tags: [DEV, TypeScript]
pin: true
math: true
mermaid: true
---
---
#### JavaScript
- <span class='fs-09'>작성된 코드를 보면 TypeScript보다 간결해 보이지만, 함수 실행 과정에서 전달해야 할 각 Type을 정확히 알지 못 할 경우 의도하지 않은 문제가 발생할 소지가 있다.</span>
###### Example
```javascript
function abcText(text, limit, symbol="..."){
    return `${String(text).slice(0, limit - 1)}${symbol}`
}
```
<span class='fs-09'>위의 함수를 `javascript`에서 실행을 하면 `Type`이 올바르지 않더라도 오류가 발생되지 않습니다.</span>
```javascript
abcTexT(100304040202, 30, 101)              // 결과값 "100304040202"
```
<span class='fs-09'>만약 아래와 같이 특정 Type의 유효성 검사를 하게 되면. Type의 문제로 오류가 발생할 소지가 있다.</span>
```javascript
function abcText(text, limit, symbol="..."){
    if(typeof text !== "string")    throw new Error("1번째 인자는 문자여야 함");
    if(typeof limit !== "number")   throw new Error("2번째 인자는 숫자여야 함");
    if(typeof symbol !== "string")  throw new Error("3번째 인자는 문자여야 함");
    return `${text.slice(0, limit - 1)}${symbol}`
}
```
아래 코드 실행시 오류가 발생합니다.
```javascript
abcTexT(100304040202, 30, 101)              
// 첫번째 인자가 숫자이기 때문에 
// 결과값은 "Uncaught Error: 1번째 전달인자 유형은 문자여야 함"와 같이 에러가 남
```
---
#### TypeScript
- <span class='fs-09'>File의 확장자가 `.ts` 되어 있음.</span>
- <span class='fs-09'>`TypeScript`는 `ECMAScript 2015(ES6)`의 새롭고 강력한 기능은 포함한 모던 `JavaScript`의 기능을 지원하여 좀 더 견고한 컴포넌드를 개발하는데 많은 도움을 줄 수 있음.</span>
##### 장점
- <span class='fs-09'>코드 량만 보면 굳이 `TypeScript`를 써야 할까 싶지만, TypeScript를 사용하면 JavaScript와 달리 코드 작성 과정에서 코드를 실시간으로 디버깅할 수 있어 매우 편리.</span>

##### 단점
1. <span class='fs-09'>자료형때문에 귀찮은 점이 있다.</span>
- <span class='fs-08'>자동으로 타입이 지정되기도 하지만, 필요한 부분은 한번 더 확인이 필요하기 때문에, Source에 빨간 줄이 많기 보여서 생산성이 떨어지기도 한다.</span>
2. <span class='fs-09'>Interface나 class의 이름때문에 오류가 생길 때도 있다.</span>
- <span class='fs-08'>같은 내용을 담고 있다 하더라도 이름이 다른 경우 문제의 야기성이 있다.</span>
- <span class='fs-08'>또란 다른 내용이 더라도 이름이 비슷한 경우도 문제가 될 수 있다.</span>
3. <span class='fs-09'>가독성이 떨어진다.</span>
4. <span class='fs-09'>결과적으로 `TypeScript`에서 `JavaScript`에서 생기는 오류를 완전히 피할 수는 없다.</span>
###### Example
```javascript
function abcText(text:string, limit:number, symbol:string="..."):string {
    return `${text.slice(0, limit - 1)}${symbol}`
}
```
<span class='fs-09'>`TypeScript`같은 경우 선언할 때부터 `DataType을 지정`하기 때문에 실행시 컴파일 과정 부터 오류가 발생.</span>
```javascript
abcTexT(100304040202, 30, 101)              
// Argument of type 'number' is not assignable to parameter of type 'string'.
```
