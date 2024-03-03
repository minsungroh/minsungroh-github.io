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
<span class="fs-05">- 작성된 코드를 보면 TypeScript보다 간결해 보이지만, 함수 실행 과정에서 전달해야 할 각 Type을 정확히 알지 못 할 경우 의도하지 않은 문제가 발생할 소지가 있다.</span>
###### Example
```javascript
function abcText(text, limit, symbol="..."){
    return `${String(text).slice(0, limit - 1)}${symbol}`
}
```
<sub>위의 함수를 `javascript`에서 실행을 하면 `Type`이 올바르지 않더라도 오류가 발생되지 않습니다.</sub>

```javascript
abcTexT(100304040202, 30, 101)              // 결과값 "100304040202"
```
<sub>만약 아래와 같이 특정 Type의 유효성 검사를 하게 되면. Type의 문제로 오류가 발생할 소지가 있다.

```javascript
function abcText(text, limit, symbol="..."){
    if(typeof text !== "string")    throw new Error("1번째 인자는 문자여야 함");
    if(typeof limit !== "number")   throw new Error("2번째 인자는 숫자여야 함");
    if(typeof symbol !== "string")  throw new Error("3번째 인자는 문자여야 함");
    return `${text.slice(0, limit - 1)}${symbol}`
}
```
<sub>아래 코드 실행시 오류가 발생합니다.
```javascript
abcTexT(100304040202, 30, 101)              
// 첫번째 인자가 숫자이기 때문에 
// 결과값은 "Uncaught Error: 1번째 전달인자 유형은 문자여야 함"와 같이 에러가 남
```
---
#### TypeScript
- <sub>File의 확장자가 `.ts` 또는 `.tsx`로 되어 있음.</sub>

##### 장점
- <sub>코드 량만 보면 굳이 TypeScript를 써야 할까 싶지만, TypeScript를 사용하면 JavaScript와 달리 코드 작성 과정에서 코드를 실시간으로 디버깅할 수 있어 매우 편리합니다.</sub>

##### 단점
1. 초반 Setting이 불편하다.
- `TypeScript`는 독자적인 언어가 아니기 때문에, 기존에 존재하는 Javascript Engine에서 실행된다.
- 이 때문에 기존적으로 설치해야 하는 항목들이 있는데.. FrameWork를 사용할때 초기 설정이 까다로운 편이다.

2. 자료형때문에 귀찮은 점이 있다.
- 자동으로 타입이 지정되기도 하지만, 필요한 부분은 한번 더 확인이 필요하기 때문에, Source에 빨간 줄이 많기 보여서 생산성이 떨어지기도 한다.

3. <span class="fs-05">Interface나 class의 이름때문에 오류가 생길 때도 있다.</span>
- <span class="fs-05">같은 내용을 담고 있다 하더라도 이름이 다른 경우 문제의 야기성이 있다.</span>
- <span class="fs-05">또란 다른 내용이 더라도 이름이 비슷한 경우도 문제가 될 수 있다.</span>

4. <span class="fs-05">가독성이 떨어진다.</span>

5. <span class="fs-05">결과적으로 `TypeScript`에서 `JavaScript`에서 생기는 오류를 완전히 피할 수는 없다.</span>

###### Example
```javascript
function abcText(text:string, limit:number, symbol:string="..."):string {
    return `${text.slice(0, limit - 1)}${symbol}`
}
```
<span class="fs-05">`TypeScript`같은 경우 선언할 때부터 `DataType을 지정`하기 때문에 실행시 컴파일 과정 부터 오류가 발생.</span>
