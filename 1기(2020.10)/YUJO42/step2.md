### 반복문?
- 반복문이란 프로그램 내에서 똑같은 명령을 일정 횟수만큼 반복하여 수행하도록 제어하는 명령문입니다.
- Javascript에는 다양한 for 반복문이 존재합니다.
- ```for (let i = 0; i < nums.length; i++) ``` 
- ```for (let num of nums)```
- ```for (let num in nums)```
- 위의 세 가지 반복문에 대해 정리하기 위한 글입니다.
___
### for 반복문
- 가장 기본적인 반복문입니다.
```javascript
const nums = [1, 2, 3, 4, 5];

for (let i = 0; i < nums.length; i++) {
  console.log('for', nums[i]);
}
> for 1
  for 2
  for 3
  for 4
  for 5
```
- 다른 언어와 마찬가지로 사용되며 저 같은 경우 자바스크립트를 배우고 한동안 ```for ...of```나 ```for ...in```을 잘 사용하지 않고 익숙한 이 방법으로 반복문을 쓰고는 했습니다.
___
### for ...of 반복문
#### 1. 일반적인 반복
- 개인적으로 반복문 중 가장 많이 사용하는 반복문입니다.
```javascript
const nums = [1, 2, 3, 4, 5];

for (const num of nums) {
  console.log('for of', num);
}
> for of 1
  for of 2
  for of 3
  for of 4
  for of 5
```


#### 2. map의 순회
  - for of는 구조분해할당 또는 ```Map```의 Method를 통해 ```Map```을 순해 할 수 있습니다.
```javascript
const map = new Map([
  ['a', 1],
  ['b', 2],
  ['c', 3],
]);

// Map의 key 순회
for (const key of map.keys()) {
  console.log(`key : ${key}`);
}
> key : a
  key : b
  key : c

// Map의 value 순회
for (const val of map.values()) {
  console.log(`val : ${val}`);
}
> val : 1
  val : 2
  val : 3

// 구조분해할당을 통한 Map의 key, value 순회
for (const [key, val] of map) {
  console.log(`key : ${key}, val : ${val}`);
}
> key : a, val : 1
  key : b, val : 2
  key : c, val : 3
```
#### 3. set 순회
- 일반적인 for문으로 순회가 불가능한 자료구조 ```set```도 순회가 가능합니다.
  - ```...``` 같은 spread 연산자를 사용하면 for문으로도 순회가 가능합니다
```javascript
const set = new Set([1, 2, 3]);


for (let i = 0; i < set.length; i++) {
  console.log('for', set[i]);
}
> 출력값 없음

for (const val of set) {
  console.log(val);
}
> 1
  2
  3
```
___
### for ...in 반복문
- for ...in 반복문의 경우 객체의 반복을 위해 만들어진 문법입니다. 
```javascript
Object.prototype.objCustom = function () {};
Array.prototype.arrCustom = function () {};

const test = [3, 5, 7];
test.foo = 'hello';

for (let val in test) {
  console.log(`for ...in ${val}`);
}
> for ...in 0
  for ...in 1
  for ...in 2
  for ...in foo
  for ...in arrCustom
  for ...in objCustom

for (let val of test) {
  console.log(`for ...of ${val}`);
}
> for ...of 3
  for ...of 5
  for ...of 7
```
- 위의 결과에서 확인할 수 있듯이 for ...in의 경우 해당 객체의 모든 열거 가능한 속성에 대해 출력합니다.
- 하지만 for ...of의 경우 ```[Symbol.iterator]```가 있는 속성에 대해서만 출력하는걸 확인할 수 있습니다.
---
### 참고자료
- [for ...of / MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for...of)
- [for ...in / MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for...in)
___
