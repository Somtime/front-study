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

</details>
