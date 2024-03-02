---
title: TypeScript 기본 정리
author: happywerrior
date: 2024-03-02 22:15:00 +0900
categories: [Blogging, Tutorial, TypeScript]
tags: [DEV]
---

#### TypeScript
- File의 확장자가 `.ts` 또는 `.tsx`로 되어 있음.

##### 장점

- JavaScript같은 경우 자료형을 지정하지 않고 사용을 하기 때문에 변하긴 하지만.. 추적이 안되는 단점이 있고, 말도 안되는 오류가 발생할 수도 있다.
- 물론 실무에서는 JavaScript를 할때 Stress Test등을 통해서 걸러지긴 하지만.. 결국은 마찬가지(개발자의 공수가 많이 들어갈 수 있다)
- JavaScript의 의 약점을 보안하기 위해서 만들어졌다고 보면 될 것이고.. 상위는 물론 JavaScript이다.

##### 단점
1. 초반 Setting이 불편하다.
- `TypeScript`는 독자적인 언어가 아니기 때문에, 기존에 존재하는 Javascript Engine에서 실행된다.
- 이 때문에 기존적으로 설치해야 하는 항목들이 있는데.. FrameWork를 사용할때 초기 설정이 까다로운 편이다.

2. 자료형때문에 귀찮은 점이 있다.
- 자동으로 타입이 지정되기도 하지만, 필요한 부분은 한번 더 확인이 필요하기 때문에, Source에 빨간 줄이 많기 보여서 생산성이 떨어지기도 한다.

3. Interface나 class의 이름때문에 오류가 생길 때도 있다.
- 같은 내용을 담고 있다 하더라도 이름이 다른 경우 문제의 야기성이 있다.
- 또란 다른 내용이 더라도 이름이 비슷한 경우도 문제가 될 수 있다.

4. 가독성이 떨어진다.

5. 결과적으로 `TypeScript`에서 `JavaScript`에서 생기는 오류를 완전히 피할 수는 없다.


```javascript
// JavaScript
let a;

a = 1;
a = true;
```

```javascript
// TypeScript
let a: number   // Red Line

a = 1;
a = true;       // Error
```

<br />

#### Example
---

##### default
```javascript
let hello: string = "helloworld!";                  // String
let num: number = 111;                              // Number
let isbit: boolean = true;                          // boolean
```

##### Array
```javascript
let arr1: number[] = [10, 20, 30]
let arr2: Array[number] = [10, 20, 30];
let arr3: Array[string] = ["hello", "world"];
let arr4: [string, number] = ["hello", 11];
```

##### Object
```javascript
let hello: object = {name: "hello", age: 11};
let person: {name:string, age:number} = {name="hello", age:11}
```

##### Function
```javascript
function add(x:number, y:number): number {return x + y};

function stringadd(firstName:string, lastname?:string){
    if(lastname){
        return firstname + " " + lastname;
    }
    else{
        return firstname;
    }
}
```

### Interface
```javascript
interface User{
    age:number;
    name:string;
}

const student: User = {name:"hello", age:11};
```

##### 함수인자
```javascript
function getUser(user: User){
    console.log(user);
}

getUser({name: "hello", age:11});
```

##### 함수 구조
```javascript
interface Add{
    (x: number, y:number): number;
}

let addFunc: Add = (a, b) => a + b;

console.log(addFunc(11, 3));
```

##### 배열
```javascript
interface StringArr{
    [index:string]: string;
}

let arr: StringArr = ["a", "b", "c"];
```

##### 객체 활용
```javascript
interface Obj{
    [key:string]:string
}

const obj: Obj{
    name1:"Hello",
    name2:"World"
}
```

##### interface 확장
```javascript
inteface Person{
    name:string;
    age:number;
}

interface Developer extends Person{
    position:string;
}

const student: Develper={
    name:"hello",
    age:11,
    position:"CIO"
}
```

##### Type
```javascript
type StrOrNum = string | number;

const str1: StrOrNum = "hello"
const str2: StrOrNum = 11;
```

### 연산자
##### 유니언 Type
```javascirpt
function strOrNum(value:string | number) {
    if(typeof value === "string"){
        value.toString();
    }
    else if(typeof value === "number"){
        value.toLocaleString();
    }
    else{
        throw new TypeError("문자열 또는 숫자를 넣어주세요~~!!!!");
    }
}
```

##### 교차 Type
```javascript
interface Person {
    name:string,
    age:number
}

interface Developer{
    name:string,
    skill:string
}

type Stu = Person & Developer;

lef devStu: Stu = {
    name : "hello",
    age: 11,
    skill: "TypeScript...."
}
```

### Class
| 접근가능성           | Public | protected | private |
| :------------------ | :-----: | :------:   | :-----:  |
| 클래스 내부          | O      | O         | O |
| 자식 클래스          | O      | O         | X |
| 클래스 인스턴스      | O       | X         | X |


```javascript
class Person{
    private name:string;
    public age:number;
    readonly log:string;

    Person(name:string, age:number){
        this.name = name;
        this.age = age;
    }
}
```

### Generic
```javascript
function logText<T>(text: T): T{
    console.log(text);
    return text;
}

logText<string>("hello world");
```

```javascript
interface Menu<T>{
    value:T;
    private:number;
}

const pizza: Menu<string> = {value:'peperoni', price:30000};
```

##### Generic Type 제한
```javascript
배열 Hit

function textLength<T>(text: T[]): T[]{
    console.log(text.length);
    return text;
}

textLength<string>(["hello", "world"]);
```

```javascript
정의된 Type

interface LengthType{
    length:number;
}

function LogTextLen<T extends LengthType>(text: T): T{
    console.log(text.length);
    return text;
}

LogTextLen("hello world")           -- 11
LogTextLen(100);                    -- Error
LogTextLen({length:100});           -- 100
```

```javascript
keyof

interface item{
    name:string;
    price:number;
    juso:string;
}

function getItemOption<T extends keyof item><itemOption: T>: T{
    return itemOption;
}

// key로만 인자 사용 가능..
getItemOption('name');
```





