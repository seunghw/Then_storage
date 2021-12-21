자바스크립트로 코테를 준비하기 시작하면서 여러 글들을 보았고 JS코테에 대한 중요한 정보들을 조금씩 모아가보려고 한다.

## 1. const, let

> `var` 만 사용하든지, `let` 과 `const` 만 사용하기

Javascript로 코딩테스트를 제출하는 사람들 중 많은 사람들의 실수가, 함수 스코프 var와 블록 스코프 const, let을 혼용하는 점이라고 한다.[자바스크립트 코딩 테스트에서 가장 많이하는 실수들](https://medium.com/%EC%98%A4%EB%8A%98%EC%9D%98-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%BD%94%EB%94%A9-%ED%85%8C%EC%8A%A4%ED%8A%B8%EC%97%90%EC%84%9C-%EA%B0%80%EC%9E%A5-%EB%A7%8E%EC%9D%B4%ED%95%98%EB%8A%94-%EC%8B%A4%EC%88%98%EB%93%A4-a10df2c884c)

```jsx
const fs = require("fs");
const input = fs.readFileSync("/dev/stdin").toString().split(" ");
const a = parseInt(input[0]);
const b = parseInt(input[1]);
console.log(a + b);
```

개인적으로 입력값은 불변값으로 다루는 것이 좋다고 생각한다. 입력값은 말그대로 문제에서 주어지는 값이므로, 이를 변경할 일은 없는 것이 일반적. 후에 for문이나 조건문 등에서 사용될 때에 입력값을 변경하여 오류가 생기는 일을 막을 수 있다. 따라서 모두 const로 변수를 선언한다.

## 2. 세미콜론

> 무조건 쓰기! 썼다 안 썼다하면 질문왔을 때 대처가 어렵다고한다.

많은 프로그래밍 언어들이 문장의 끝에 세미콜론을 붙이는 방식을 채택하고 있다. 자바스크립트는 세미콜론에 비교적 자유롭다. 세미콜론을 붙여도 되고, 붙이지 않아도 된다. 끝에 세미콜론을 붙이는 것이 거의 국룰이 되긴 했지만, 그래도 일부 라이브러리는 세미콜론을 붙이지 않는 컨벤션을 갖고 있다고 한다.

예시) 이렇게 썼다 안 썼다하지 말자.

```jsx
function mixUsageSemicolons() {
  const students = ['James', 'Jane', 'Mike'];

  for (let i = 0; i < students.length; i += 1) {
    if (students[i] === 'Jane') {
      console.log('I found Jane!')
    } else {
      console.log(`It's ${students[i]), not Jane`);
    }
  }

  console.log('Printed all students name')
}
```

세미콜론을 왜 써야하는가에 대한 글

[https://www.freecodecamp.org/news/codebyte-why-are-explicit-semicolons-important-in-javascript-49550bea0b82/](https://www.freecodecamp.org/news/codebyte-why-are-explicit-semicolons-important-in-javascript-49550bea0b82/)

## 3. 일치연산자는 무조건 는는는(===)

> == 보다 ===이 문제가 생길 여지가 적다.

이 부분 역시 항상 `===` 을 사용하는 것이 기준 국룰이라고 한다. 그 이유는 `==` 을 사용했을 경우 [예기치 못한 경우](https://dorey.github.io/JavaScript-Equality-Table/)에서 `true`, `false` 가 결과로 반환될 수 있기 때문이다. 해서, 정말 특별하게 반드시 `==` 을 사용해야하는 경우가 아니라면, `===` 을 사용하는 것이 바람직하다.

예시)

```jsx
function strictComparison(names) {
  for (let i = 0; i < names.length; i += 1) {
    if (names[i] === "Jane") {
      console.log("I found Jane!");
    }
  }
}
```

## **문자열**

### **대소문자 구별**

### **1. toLowerCase(), toUpperCase()**

문자의 대문자, 소문자 여부를 구분 할 수 있는 함수입니다. **대문자라면,** 혹은 **소문자라면** 이라는 조건식에 주로 많이 사용됩니다.

주로 for 문과 같이 사용됩니다. 사용 방법은 문자열에 대해서 한 개의 문자를 뽑은 후 str.toLowerCase() 혹은 str.toUpperCase() 로 대문자나 소문자로 치환하고 if 문을 통해 비교하는데 사용합니다.

```jsx
// 만약 소문자라면, 답을 하나 더해줍니다.
if (x == x.toLowerCase()) answer++;
// 대문자라면, 답을 하나 더해줍니다.
if (x == x.toUpperCase()) answer++;
```

대문자이거나 소문자라면 True 를 return 하는 함수가 아닙니다. 소문자라면 대문자, 대문자라면 소문자로 만들어 주는 함수이니 isUpper, isLower 로 잘못 아시면 안됩니다.

```jsx
str = "abc";
console.log(str[0].toUpperCase()); // A 출력!
```

### **2. charCodeAt()**

문자 하나를 아스키 코드로 바꿔주는 함수입니다. 마찬가지로 대문자나 소문자 여부를 판단하기 위해서 사용되는 기법중 하나입니다. 아래의 코드처럼 사용합니다.

```jsx
// num 에 문자 chr 의 아스키 코드를 대입합니다.
let num = chr.charCodeAt();
// 아스키 코드에서 65는 'A', 90은 'Z' 입니다. 그렇다면 아래 코드는 대문자라면, 이 되겠네요.
if (num >= 65 && num <= 90) answer++;
```

소문자는 97 ~ 122 의 아스키코드를 가지고 있고 대문자는 65 ~ 90 의 아스키 코드를 가지고 있습니다. 이를 통해 얻을 수 있는 간단한 팁 중 하나는 소문자에서 대문자로 변경하고 싶으면 -32, 대문자에서 소문자로 변경하고 싶으면 +32 를 하면 됩니다!

### **문자 찾기**

### **1. split()**

지정한 구분자를 통해 문자열을 여러개로 나눌 수 있습니다. 이때의 반환값은 배열입니다.

```jsx
const str = "Progwon is a boy";

const words = str.split(" "); // [ 'progwon', 'is', 'a', 'boy' ]
```

split() 을 사용하면 원하는 문자의 개수를 찾을 수도 있습니다. 위 코드는 공백을 기준으로 문자열을 나눴습니다. 다르게 해석하면 공백을 제외한 문자나 문자열의 개수가 저장되게 됩니다. 이 배열의 length 에서 -1 을 하게 된다면 원하는 문자나 문자열의 개수를 찾는게 가능합니다.

```jsx
const str = "Progwon is a boy";

const words = str.split(" "); // [ 'progwon', 'is', 'a', 'boy' ]

console.log(words.length - 1); // 3 (공백의 개수)
```

### **2. substring()**

시작 인덱스부터 종료 인덱스 전(전까지가 중요합니다. 포함하지 않습니다.)까지의 부분 문자열을 반환합니다.

```jsx
const str = "progwon is a boy";
console.log(str.substring(0, 4)); // prog (0 ~ 3 까지)
```

만약 종료 인덱스와 시작 인덱스가 같으면 빈 문자열을 반환합니다.

```jsx
const str = "progwon is a boy";
console.log(str.substring(0, 0)); // 빈 문자열
```

만약 종료 인덱스가 시작 인덱스보다 작은 경우 두 인자를 바꾼것처럼 작동합니다.

```jsx
const str = "progwon is a boy";
console.log(str.substring(4, 0)); // prog 마치 0, 4 처럼 작동!
```

종료 인덱스 없이 시작 인덱스만 있으면 시작 인덱스부터 끝까지 반환합니다.

```jsx
const str = "progwon is a boy";
console.log(str.substring(0)); // 'progwon is a boy'
```

## **배열**

### **배열에 값 추가하기**

### **1. Array.push()**

Array.push() 는 배열의 끝에 원하는 값을 추가하고 싶을 때 사용합니다.

```jsx
var arr[1, 2, 3];

arr.push(4)
console.log(arr) // [1, 2, 3, 4]
```

### **2. Array.unshift()**

Array.unshift() 는 push() 와 반대로 맨 앞에 원하는 값을 추가하고 싶을 때 사용합니다.

```jsx
var arr[1, 2, 3];

arr.unshift(4)
console.log(arr) // [4, 1, 2, 3]
```

### **3. Array.splice()**

Array.splice() 는 원하는 위치에 1개 이상의 원소를 추가할 수 있습니다. arr.splice('인덱스 위치', 0, ["값1", "값2"]) 처럼 사용합니다.

```jsx
var arr[1, 2, 3];

arr.splice(0, 0, 4)
console.log(arr) // [4, 1, 2, 3]
arr.splice(0, 0, 1, 2, 3, 4)
console.log(arr) // [1, 2, 3, 4, 4, 1, 2, 3]
```

### **배열 복사하기**

배열 복사시에 가장 많이 하는 실수가 단순히 배열을 새로운 배열에 그대로 할당해주는 것입니다. 이 경우에는 치명적인 문제가 발생할 수 있습니다.

```jsx
let arr = [1, 111, 4, 5, 27];
let arr1 = arr;

console.log(arr1); // [ 1, 111, 4, 5, 27 ]

arr.sort((a, b) => a - b);

console.log(arr1); // [ 1, 4, 5, 27, 111 ]
```

분명 arr1 에는 어떠한 행동을 취하지 않았음에도 불구하고 arr1 의 값이 변경되었습니다. 이는 **얕은 복사**가 일어났기 때문입니다. 이때는 배열의 참조값이 전달되기 때문에 만약 원본 배열이 바뀌게 되면 원치 않는 변경이 일어날 수 있습니다. 이러한 실수를 방지하기 위해서는 아래와 같은 방법을 사용하는 것이 좋습니다.

### **1. slice()**

slice() 를 사용하면 배열을 복사해서 생성해줍니다. 주의할 점은, 만약 참조형 요소가 존재한다면 얕은 복사가 진행된다는 점입니다. 하지만 알고리즘 문제 풀이시에는 slice() 정도의 복사만 사용해도 거의 아무런 문제 없이 사용이 가능합니다. 사용 방법은 아래와 같습니다.

```jsx
let arr = [1, 111, 4, 5, 27];
let arr1 = arr.slice();

console.log(arr1); // [ 1, 111, 4, 5, 27 ]

arr.sort((a, b) => a - b);

console.log(arr); // [ 1, 4, 5, 27, 111 ]

console.log(arr1); // [ 1, 111, 4, 5, 27 ]
```

## **Math**

### **최대/최소 구하기**

### **1. Math.max()**

Math.max 를 통해서 주어진 수의 최대값을 구하는 것이 가능합니다. 주의할점은 **마치 배열을 넣으면 원소중의 최대값을 구해줄 것 같지만 그렇지 않다는 것입니다.** 이때는 **스프레드 연산**을 사용해서 배열의 원소들을 풀어주어야 합니다.

```jsx
let max = Math.max(5, 7, 33, 3, 3, 9, 11); // 33

// 배열을 사용하는 경우
arr = [5, 7, 33, 3, 3, 9, 11];
let max = Math.max(...arr); // ... 이 배열 앞에 있으면 안의 원소들을 풀어줌.
```

### **2. Math.min()**

Math.min 를 통해서 주어진 수의 최소값을 구하는 것이 가능합니다. 마찬가지로 **마치 배열을 넣으면 원소중의 최대값을 구해줄 것 같지만 그렇지 않습니다.** 역시 **스프레드 연산**을 사용해서 배열의 원소들을 풀어주어야 합니다.

```jsx
let min = Math.min(5, 7, 33, 3, 3, 9, 11); // 3

// 배열을 사용하는 경우
arr = [5, 7, 33, 3, 3, 9, 11];
let min = Math.min(...arr); // ... 이 배열 앞에 있으면 안의 원소들을 풀어줌.
```

## **정렬**

### **1. 배열 내부의 수들 정렬하기**

자바스크립트의 배열이 제공하는 sort 를 사용해보면 정상적으로 정렬이 되는것처럼 보입니다. 하지만 **사실 자바스크립트는 문자열로 바꾼 후에 정렬을 진행**합니다. 만약 number 값들을 배열이 제공하는 sort 메서드를 통해서 정렬하면 아래와 같은 결과가 나오게 됩니다.

```jsx
const arr = [1, 3, 4, 5, 6, 11, 111, 1111];
console.log(arr.sort());

// 결과
[1, 11, 111, 1111, 3, 4, 5, 6];
```

원하는 결과를 만들기 위해서는 sort() 메서드에 compare 함수, 즉 비교 함수를 인수로 넣어줘야 합니다. 이때 가장 많이 사용하는 오름차순과 내림차순을 구현하면 아래와 같습니다.

```jsx
const arr = [1, 3, 4, 5, 6, 11, 111, 1111];

console.log(arr.sort((a, b) => a - b)); // 오름차순
console.log(arr.sort((a, b) => b - a)); // 내림차순

// 결과
[1, 3, 4, 5, 6, 11, 111, 1111][(1111, 111, 11, 6, 5, 4, 3, 1)];
```

### **2. 2차원 배열 내부의 수들 정렬하기**

1차원 배열의 정렬이 아닌 2차원 배열의 정렬은 조금 다른 방식으로 구현합니다. 이때 인덱스를 함께 기입해줍니다.

### **1. 오름차순 정렬하기**

```jsx
const arr = [
  [0, 1],
  [3, 2],
  [10, 1],
  [7, 10],
];

arr.sort((a, b) => a[0] - b[0]); // 2차원 배열의 0 번째 인덱스를 기준으로 오름차순 정렬
arr.sort((a, b) => a[1] - b[1]); // 2차원 배열의 1 번째 인덱스를 기준으로 오름차순 정렬

// 결과
[
  [0, 1],
  [3, 2],
  [7, 10],
  [10, 1],
][([10, 1], [7, 10], [3, 2], [0, 1])];
```

### **2. 내림차순 정렬하기**

```jsx
const arr = [
  [0, 1],
  [3, 2],
  [10, 1],
  [7, 10],
];

arr.sort((a, b) => b[0] - a[0]); // 2차원 배열의 0 번째 인덱스를 기준으로 내림차순 정렬
arr.sort((a, b) => b[1] - a[1]); // 2차원 배열의 1 번째 인덱스를 기준으로 내림차순 정렬

// 결과
[
  [10, 1],
  [0, 1],
  [3, 2],
  [7, 10],
][([7, 10], [3, 2], [10, 1], [0, 1])];
```
