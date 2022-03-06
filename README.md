# Front End Study

##### TODO : JavaScript bind, call, apply, new

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

#### 즉시 실행 함수 표현식 (Immediately-Invoked Function Expressions)

```
for (var i = 0; i < length; i++) {
  (function(j) {
    setTimeout(() => {
      console.log(j);
    }, (j + 1) * 1000);
  })(i);
}
```

<i>위와같은 문제는 이처럼 함수로 감싸서 해결할 수 있음</i>

<br>

### 2022-03-02

#### 실행 컨택스트 (Execution Context)

```
실행 컨택스트 : 실행 가능한 코드를 형상화하고 구분하는 추상적인 개념
             : 식별자 결정을 더욱 효율적으로 결정하기 위해 관련 정보를 모아 제공하는 객체
종류
- 전역 컨택스트 (Global Context)
- 함수 컨택스트 (Functional Context)
Global Context -> Function Context 순으로 스택-LIFO(Last In First Out)-으로 쌓임
Functional Context 는 함수 사용 후 소멸 (Closure 제외)

객체
- Variable Object
  Variable (Global Object - Global Context / Activation Object - Functional Context)
  Parameter, Arguments (Functional Context)
  함수 선언식 (표현식 제외 ex: const func = function() {})
- Scope Chain
  Execution Context 가 참조할 수 있는 변수, 함수 선언 등의 정보를 담고 있는 Global Object, Activation Object 를 가리키는 List 형태
  Activation Object -> Global Object 순으로 가리키는 형태 (하위 객체 -> 상위 객체)
  Javascript 엔진은 Scope Chain 을 통해 하위 -> 상위 객체를 순차적으로 탐색하여 변수, 함수 등을 찾음
- this
  this 의 Property 는 Global FunctionInvocation, (call, apply, bind), Construction, MethodInvocation 패턴으로 결정
```

##### Reference

##### <a>https://poiemaweb.com/js-execution-context</a>

##### <a>https://velog.io/@stampid/Execution-Context%EC%8B%A4%ED%96%89-%EC%BB%A8%ED%85%8D%EC%8A%A4%ED%8A%B8%EB%9E%80</a>

##### <a>https://ko.javascript.info/recursion#ref-27</a>

<br>

### 2022-03-03

#### 구조 분해 할당

```
let arr = [1, 2, 3, 4, 5];
let one = arr[0];
let two = arr[1];
let three = arr[2];
let four = arr[3];
let five = arr[4];
==
let [ one, two, three, four, five ] = arr;

중간 값을 안 받을 땐, 해당 인덱스 비워주면 됨

let [ one, , , four, five ] = arr;
```

```
let options = {
  title: "Menu",
  height: 200,
  width: 100
};

let {...rest} = options; // 이렇게 받아주면

rest = {
  title: "Menu",
  height: 200,
  width: 100
}; // rest 에 다 들어감

let {...rest} = options; // 이 경우엔

title = "Menu";

rest = {
  height: 200,
  width: 100
}; // 이처럼 들어감
```

<i>중첩 구조 분해</i>

```
let options = {
  size: {
    width: 100,
    height: 200
  },
  items: ["Cake", "Donut"],
  extra: true
};

let {
  size: {
    width, => *
    height => *
  },
  items: [item1, item2], => *
  title = "Menu" => *
} = options;

```

<i>이렇게 할 경우에는 size, itmes, extra 를 제외한 width, height, item1, item2, title 변수가 선언 됨</i>

<br>

### 2022-03-04

#### Shllow Copy, Deep Copy, Reference

```
const object = {
	nested: {
		key: value
	}
};
```

<i>Shllow Copy</i>

```
한 단계까지는 복사하지만 그 이후의 값은 참조

const copy = { ...object };
```

<i>Deep Copy</i>

```
중첩된 모든 객체를 복사

const copy = JSON.parse(JSON.stringify(object));
```

##### Reference

##### <a>https://roseline.oopy.io/dev/javascript-back-to-the-basic/shallow-copy-deep-copy</a>

##### <a>https://helloinyong.tistory.com/267</a>

<br>

### 2022-03-06

#### this

자바스크립트에서 this 의 기본값은 window
```
console.log(this); // window
```

<br>

생성자나 객체 내의 함수의 경우에 this 는 해당 인스턴스 객체를 참조
```
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.sayHi = function() {
  console.log(this.name, this.age);
}
```

EventListener, Jquery 함수에서는 해당 태그 객체를 참조
```
document.body.onclick = function() {
  console.log(this); // <body>
}

$('div').on('click', function() {
  console.log(this); // div
});
```

하지만 그 내부 함수에서는 this 를 명시적으로 전달하지 않아서 window 를 참조  
여기에서 화살표 함수를 사용하게 되면 이는 상위 객체의 this를 가져오기 때문에 정상적으로 this 를 참조해줄 수 있음
```
document.body.onclick = function() {
  console.log(this); // <div>
  const inner = () => {
    console.log('inner', this); // inner <div>
  }
  inner();
});
```
##### Reference

##### https://www.zerocho.com/category/JavaScript/post/5b0645cc7e3e36001bf676eb

<br>


</details>
