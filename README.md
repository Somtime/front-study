# Front End Study

<details open>
<summary>ZeroCho ES2021 자바스크립트 강좌</summary>

<br>

### 2022-02-25

<br>

#### 화살표 함수 (Arrow Function)

```
(arguments) => {
  return arguments;
}

  => (arguments) => return arguments;

  위처럼 바로 return 해주는 경우 {} 생략 가능
```

<br>

#### 리스너 함수 (Callback Function)

```
TagSelector.addEventListener('eventName', callbackFuncName);
const callbackFuncName = (event) => {
  console.log(event.target.value);
}
```

<br>

#### 고차 함수 (High Order Function)

```
const func = () => {
  return () => {
    console.log("High Order Function");
  }
}

const innerFunc = func();
```

<i>이런식의 함수와 동일하게 실행됨</i>

```
const innerFunc = () => {
  console.log("High Order Function");
}
```

<i>다음과 같이 리스너 함수에서 매개변수를 넣어서 사용이 가능해짐</i>

```
const callbackFuncName = (argumentName) => {
  return () => {
    console.log(argumentName);
  }
}
TagSelector.addEventListener('eventName', callbackFuncName(argument));
```

<i>바로 return 시 다음 처럼 return 생략 가능</i>
<span style="font-size: 8px; color: gray;">화살표 함수 (Arrow Function) 참조</span>

```
const callbackFuncName = (argumentName) => () => {
  console.log(argumentName);
}

TagSelector.addEventListener('eventName', callbackFuncName(argument));
```


<br>

### 2022-02-27

<br>

#### 피셔-예이츠 셔플 (Fisher-Yates Shuffle)
```
// While 문 사용시
const array =  Array(45).fill().map((value, index) => index + 1);
const shuffle = [];
  
while (array.length > 0) {
  let random = Math.floor(Math.random() * array.length);	// random index 생성
  let tmp = array.splice(random, 1);	// array 배열에서 선택된 index에 해당하는 값을 제거하고 tmp 에 넣음
  shuffle.push(tmp[0]);	// shuffle 에 해당 값을 넣어줌
}

// For 문 사용시 
for (let i = array.length; i > 0; i--) {
  let random = Math.floor(Math.random() * i);
  let tmp = array.splice(random, 1);
  shuffle.push(tmp[0]);
}
```

<br>

#### let, var
```
for (let i = 0; i < length; i++) {
    setTimeout(() => {
    console.log(i);
  }, (i + 1) * 1000);
}
```
<i>let 으로 실행하는 경우</i> 이상 없이 실행됨
```
for (var i = 0; i < length; i++) {
  setTimeout(() => {
    console.log(i);
  }, (i + 1) * 1000);
}
```
<i>var 으로 실행하는 경우</i> var = length 에서 고정되어 출력됨

```
let : 블록 스코프 (block scope)
let 은 if, while, for, forEach, 함수 등 블록 내에서만 유효
var : 함수 스코프 (function scope)
var 은 if, while, for, forEach 등 블록 내에서 선언되어져도 그 외에서 접근이 가능하고 함수 내에서 사용했을 경우는 함수 내에서만 접근이 가능
```

<br>

#### 클로저 (Closure)
```
for (var i = 0; i < length; i++) {
  (function(j) {
    setTimeout(() => {
      console.log(j);
    }, (j + 1) * 1000);
  })(i);

  // TODO : Closure 알아보기
}
```
<i>위와같은 문제는 이처럼 함수로 감싸서 해결할 수 있음</i>
</details>
