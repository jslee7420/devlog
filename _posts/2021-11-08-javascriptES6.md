---
title: "자바스크립트 ES6 새로운 문법"
excerpt: "ES5와의 차이 비교"

categories:
  - TIL
tags:
  - [javascript]

toc: true
toc_sticky: true

date: 2021-11-08
last_modified_at: 2021-11-08
---

자바 스크립트 ES5와 ES6 차이점 정리

## 1. let & const

- ES5
  - var로 변수를 선언
- ES6
  - let: 값이 변하는 변수 선언, 동일한 변수 중복 선언 불허
  - const: 상수값 선언 시 사용

```javascript
// ES 5
var a = 10;
var test = function () {
  console.log(a);
  var b = "result : ";
  for (var i = 1; i <= 5; i++) {
    console.log(`${b} : ${i}`);
  }
  console.log(i);
};

test();
test = "hello";
// test(); // 오류 발생

var a = "haha";
console.log(a);

//ES 6
let a = 10;
const test = function () {
  console.log(a);
  let b = "result : ";
  for (let i = 1; i <= 5; i++) {
    console.log(`${b} : ${i}`);
  }
  // console.log(i);
};

test();
test = "hello";
// test(); // 오류 발생

// let a = "haha"; // 오류 발생
console.log(a);
```

## 2. 객체 선언

- 객체 선언 방식의 유연성 증가

```javascript
// ES5
// var name = "김재환";
// var age = 26;
// var person = {
//     name : name,
//     age : age,
//     gender : "M",
//     increaseAge: function(){
//         this.age++;
//     }
// };
// person.increaseAge();
// console.log(person);

// ES6
let name = "김재환";
let age = 26;
let person = {
  name,
  age,
  gender: "M",
  increaseAge() {
    this.age++;
  },
};
person.increaseAge();
console.log(person);
```

## 3. destructing

- 비구조화를 통해 배열 또는 객체의 값을 새 변수에 더 쉽게 할당 가능

```javascript
// ES5
// var arr = [10,20,30];
// var a = [0];
// var b = [1];

// var person = {name:'김재환', age:26, gender:'M'};
// var name = person.name;
// var age = person.age;

// console.log(`${a}, ${b}, ${name}, ${age}`);

// ES6
let arr = [10, 20, 30];
let [a, b] = arr;

let person = { name: "김재환", age: 26, gender: "M" };
let { age: c, name: n } = person;

// console.log(`${a}, ${b}, ${name}, ${age}`);
console.log(`${a}, ${b}, ${n}, ${c}`);

print(person);

function print({ name, age }) {
  console.log(`print : ${name}, ${age}`);
}
```

## 4. spread

- spread로 기존 객체를 조합한 새로운 객체 생성이 간편해짐

```javascript
// ES 5
// var person = {name:'김재환', age:26};
// var info = {tel: '010-111-2222', address:'서울 강서구'};

// var person2 = {name:person.name, age:person.age};
// var person3 = {name:person.name, age:person.age, tel : info.tel, address : info.address};

// ES 6
let person = { name: "김재환", age: 26 };
let info = { tel: "010-111-2222", address: "서울 강서구" };

let person2 = { ...person };
let person3 = { ...person, ...info };

console.log(person2);
console.log(person3);
```

## 5. for of

- for of 구문으로 반복분에서 배열의 원소에 바로 접근

```javascript
// ES 5
// var arr = [10,20,30];
// for (index in arr) {
//    console.log(arr[index]);
// }

// ES 6
let arr = [10, 20, 30];
for (item of arr) {
  console.log(item);
}
```

## 6. function default parameter

- 함수의 매개변수에 기본값 설정 가능

```javascript
// ES5
// function myFunc(name, age){
//     console.log(`${name}, ${age}`);
// }

// ES 6
function myFunc(name = "김싸피", age = 1) {
  console.log(`${name}, ${age}`);
}

myFunc();
myFunc("김재환");
myFunc("김재환", 26);
```

## 7. Arrow function

- 화살표 함수로 더 쉽게 함수 표현가능
  - 함수의 내용이 리턴문 하나인 경우 중괄호와 return 생략 가능
- 메소드에서 this가 메소드를 호출하는 객체를 가르키지만 arrow function에서는 this가 정의되지 않아 가장 상위 객체인 window 객체를 가르킴
- js에서 this 참고 https://nykim.work/71

```javascript
// ES 5
// var sum = function(a,b){
//     return a+b;
// }

// ES 6
// const sum = (a,b)=>{
//     return a+b;
// }
const sum = (a, b) => a + b;
const totalSum = (n) => {
  let res = 0;
  for (let i = 1; i <= n; ++i) {
    res += i;
  }
  return res;
};
console.log(sum(1, 2));
console.log(totalSum(10));

let arr = [10, 24, 67, 100];
// ES5
// let newArr = arr.filter(function(item){
//     return item%2==0;
// });
// ES6
let newArr = arr.filter((item) => item % 2 == 0);
console.log(newArr);

// ES5
// var person = {
//     name : '김재환',
//     age : 26,
//     gender : "M",
//     increaseAge: function(){
//         console.log(this);
//         this.age++;
//     }
// };

// ES6 오류
let person = {
  name: "김재환",
  age: 26,
  gender: "M",
  increaseAge: () => {
    console.log(this);
    this.age++; // arrow function에서 this는 window 객체, this가 정의되지 않으므로 가장 상위인 window 객체를 가르킴
  },
};

person.increaseAge();
console.log(person);
```

## 8. Module

- 재사용 가능한 코드 조각
- 모듈은 세부 사항을 캡슐화하고 공개가 필요한 API만을 외부에 노출

```html
// index.html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <script type="module" src="./main.js"></script>
  </body>
</html>
```

- script 태그에서 type 속성을 module로 지정하여 불러옴

```javascript
// main 모듈
import { cube, person } from "./mymodule1.js";
import calcutil from "./calcmodule.js";

console.log(`main module : ${cube(3)}, ${person.name}`);
console.log(calcutil.sum(2, 3));
console.log(calcutil.sub(20, 3));
```

- import 문으로 모듈에서 다른 모듈을 사용가능
- 사용할 객체를 지정

```javascript
// export function cube(x) {
//     return x * x;
// }

// export let person = {
//     name: '김재환',
//     age: 26,
// };

function cube(x) {
  return x * x;
}

let person = {
  name: "김재환",
  age: 26,
};

console.log(`mymodule1 ${person.name}, ${cube(2)}`);

export { cube, person };
```

- export 키워드로 외부로 노출할 객체를 지정
- 각각의 객체에 export 키워드를 붙일 수도 있고 여러 객체에 대해 한번에 export 지정을 할 수도 있음
- export가 붙지 않은 출력문은 외부에서 조작 불가능

```javascript
// calcmodule
export default {
  sum(a, b) {
    return a + b;
  },
  sub(a, b) {
    return a - b;
  },
};
```

- export default로 지정한 내용은 외부에서 import시 이름 지정 가능
