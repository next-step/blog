[https://www.youtube.com/watch?v=W5EszIn298w&list=PLjKaR3gonylNsEnSLeh0iS-DeF2k8i6TV&index=3](https://www.youtube.com/watch?v=W5EszIn298w&list=PLjKaR3gonylNsEnSLeh0iS-DeF2k8i6TV&index=3)

집중을 위한 해변파도소리

# 자바스크립트 sort 메소드

---

그동안 자주 사용하면서도 두루뭉술하게 알고있었던 sort 메소드에 대해서 정리해보았습니다

## 특징

- 원배열을 변환하여 반환때문에 불변성을 유지하고 싶으면 복사해서 사용
- 배열이므로 얕은 또는 깊은 복사 필요

## **arr.sort([compareFunction])**

- compareFunction 특징 : **정렬 순서를 정의하는 함수**
  - 이 값이 생략되면, 배열의 element들은 문자열로 취급되어, 유니코드 값 순서대로 **오름차순** 정렬됩니다.
  - 이 함수는 두 개의 배열 element를 파라미터로 입력 받습니다.
  - 이 함수가 a, b 두개의 element를 파라미터로 입력받을 경우,
  - 이 함수가 리턴하는 값이 0보다 작을 경우,  a가 b보다 앞에 오도록 정렬하고,(0보다 작으면 a,b순서)
  - 이 함수가 리턴하는 값이 0보다 클 경우, b가 a보다 앞에 오도록 정렬합니다.(0보다 크면 b,a순서
  - 만약 0을 리턴하면, a와 b의 순서를 변경하지 않습니다.

```jsx
function compare(a, b) {
	if (a < b) {
		return -1; // a,b 순서 유지
	}
	if (a > b) {
		return 1; // b,a 순서로 변환
	}
	// a, b 같을 때
	return 0;
}

// 오름차순
```

## 원소의 타입별 정렬하기

### 타입 : Number

- compareFunction을 안 넣었을때

```jsx
const arr = [2, 1, 3, 10];
arr.sort();
console.log(arr)
// [1,10,2,3];
두자리 이상인 숫자가 입력값일 경우 오류
```

- 숫자 오름차순 정렬

```jsx
arr.sort((a, b) => {
  if (a < b) {
    return -1
  }
  if (a > b) {
    return 1
  }
  return 0
})

좀 더 간단히 표현하면

arr.sort((a,b) => a - b) // '알파벳 순서가 오름차순'으로 외우면 편함
```

- 숫자 내림차순 정렬

```jsx
arr.sort((a, b) => b - a); // '알파벳 순서가 내림차순'으로 외우면 편함
```

### 타입 : String

- compareFunction을 안 넣었을때

```jsx
const arr = ['banana', 'b', 'Boy'];
arr.sort();

console.log(arr)
// ['Boy','b','banana']
대소문자가 구분되어 정렬
```

- 문자열 오름차순으로 정렬(대소문자 구분없이)

```jsx
const arr = ["banana", "b", "Boy"];

arr.sort((a, b) => {
	const upperCaseA = a.toUpperCase(); // 또는 toLowerCase() 사용가능
	const upperCaseB = b.toUpperCase();

	if (upperCaseA > upperCaseB) return 1;
	if (upperCaseA < upperCaseB) return -1;
	if (upperCaseA === upperCaseB) return 0;
});

console.log(arr);
// ['b','banana','Boy']
```

- 문자열 내림차순으로 정렬(대소문자 구분없이)

```jsx
const arr = ["banana", "b", "Boy"];

arr.sort(function (a, b) {
	const upperCaseA = a.toUpperCase();
	const upperCaseB = b.toUpperCase();

	if (upperCaseA < upperCaseB) return 1;
	if (upperCaseA > upperCaseB) return -1;
	if (upperCaseA === upperCaseB) return 0;
});

console.log(arr);
// ['Boy','banana','b']
```

### 타입 : Object

- 국어점수 내림차순 정렬

```jsx
const arr = [
	{
		name: "아메리카노",
		korean: 50,
		english: 40,
		math: 30,
	},
	{
		name: "에스프레소",
		korean: 50,
		english: 60,
		math: 40,
	},
	{
		name: "카페라테",
		korean: 80,
		english: 70,
		math: 40,
	},
];

arr.sort((a, b) => b.korean - a.korean);
```

- 국어점수 내림차순, 영어점수 올림차순 정렬(코딩테스트에서 유용)

```jsx
arr.sort((a, b) => {
	if (a.korean > b.korean) return -1; // 위에 있는 조건일 수록 우선순위가 높음
	if (a.korean < b.korean) return 1;
	if (a.english > b.english) return 1;
	if (a.english < b.english) return -1;
});

또는 삼항연산자를 사용하면(return 깜빡하고 표기안함 주의)

arr.sort((a, b) => {
  return a.korean > b.korean ? -1 : a.korean < b.korean ? 1 : a.english < b.english ? -1 : a.english > b.english ? 1 : 0
})
```

- sort 메소드는 quicksort 알고리즘을 사용했었으나, 동일한 값의 요소가 중복되어 있을 때 초기 순서와 변경될 수 있는 불안정한 정렬 알고리즘으로 알려져 있다. ECMAScript 2019(ES10)에서는 timsort 알고리즘을 사용하도록 바뀌었다.

### Tip!

- 배열복사시 = 사용하지 말고, **얕은 또는 깊은 복사**를 사용
- 삼항연산자 사용시 **return** 을 꼭 표기하자
- 오른차순으로 정렬뒤 **.reverse()**를 붙이면 내림차순으로 정렬된다.

혹시 오류나 개선할 점이 있으시면 알려주세요.

## 참고

- 모던 자바스크립트 Deep Dive, 이웅모, 위키북스 p532
- [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/sort](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
- [https://fluorite94.tistory.com/220](https://fluorite94.tistory.com/220)
- [http://yoonbumtae.com/?p=1237](http://yoonbumtae.com/?p=1237)
- [https://hianna.tistory.com/409](https://hianna.tistory.com/409)
