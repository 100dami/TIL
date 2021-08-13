## 동기식 (Synchronous) vs 비동기식 (Asynchronous)  

### 동기식 (Synchronous)
먼저 시작된 하나의 작업이 끝날 때까지 다른 작업을 시작하지 않고 기다렸다가 다 끝나면 새로운 작업을 시작하는 방식    
``` 동기식 처리 ``` : 작업이 직렬로 배치되어 실행되며 작업 실행의 순서가 확실히 정해져 있는 것

### 비동기식 (Asynchronous)
동기식과 반대로 먼저 시작된 작업의 완료 여부와는 상관없이 새로운 작업을 시작하는 방식    
``` 비동기식 처리 ``` : 작업이 병렬로 배치되어 실행되며 작업의 순서가 확실하지 않아 나중에 시작된 작업이 먼저 끝나는 경우도 발생 함

### 우리가 js 에서 **비동기식 처리** 를 사용하는 이유
자바스크립트는 Single Thread 언어이다.    
즉, 이벤트를 처리하는 Call Stack이 하나뿐인 언어   
따라서 여러가지 이벤트를 처리할 때에 동기적으로 처리하게 된다면 하나의 이벤트라 모-두 처리될 때까지 다른 어떤 업무도 수행하지 못하는 현상이 일어나게 된다.  

### js의 비동기 처리

### 1. 콜백 함수 사용
``` 콜백 함수 ``` : 파라미터로 함수를 전달하는 함수
``` js
function whatYourName(name, callback) {
    console.log('name: ', name);
    callback();
}

function finishFunc() {
    console.log('finish function');
}

whatYourName('dami', finishFunc);

<결과>
name: dami
finish function
```
 ##### 콜백 지옥
 ``` js
 function add(x, callback) {
    let sum = x + x;
    console.log(sum);
    callback(sum);
}

add(2, function(result) {
    add(result, function(result) {
        add(result, function(result) {
            console.log('finish!!');
        })
    })
})

<결과>
4
8
16
finish!!
```
=> 콜백 함수를 남용하게 되면 가독성과 에러 처리 등에서 불편함이 발생 그래서 우리는

### [Promise](https://github.com/100dami/TIL/blob/master/NodeJs/promise.md) 사용
-> Promise에 대한 내용은 위 링크에 더 자세히 있다!!
``` js
function add(x) {
    return new Promise((resolve, reject) => {
        let sum = x + x;
        console.log(sum);
        resolve(sum);
    })
}

add(2).then(result => {
    add(result).then(result => {
        add(result).then(result => {
            console.log('finish!!');
        })
    })
})

<결과>
4
8
16
finish!!
```
``` js
new Promise((res, rej) => {
    console.log('Initial');

    res(); // resolve된 후 then 실행
})
.then(() => {
    throw new Error('Something failed');
        
    console.log('Do this'); // error 발생으로 실행되지 않는다.
})
.catch(err => {
    console.log(err); // throw new Error의 인자 값이 넘어온다. 
})
.then(() => {
    console.log('Do this, whatever happened before'); // catch 구문 이후 chaining
});


// 출력값
Initial
Something failed // ERROR
Do this, whatever happened before // catch 메소드 이후 then 메소드 실행

```

### Async/await
**기존 Promise와의 차이점**   
가장 큰 차이점은 위에서 배웠던 resolve, reject, then, catch를 쓰지 않는다는 것..!

- Async 사용 코드 예시
``` js
// async 키워드만 붙이면 된다.
async function hello() {
  return 'Hello';
}

function callHello() {
  const r = hello();
  console.log(r); 
}

callHello();

<결과>
# 시작
Promise { 'Hello' }
# 끝
```
하지만 나는 객체 형태의 Promise { 'Hello' }가 아니라 그 안에 있는 String 형태의 Hello를 출력하고 싶다.

- await 사용 코드 예시 
``` js
async function hello() {
  return 'Hello';
}

// (2) 새로 추가된 async 키워드
async function callHello() {
  // (1) 새로 추가된 await 키워드
  const r = await hello();
  console.log(r);
}

callHello();

<결과>
# 시작
Hello
# 끝
```
**조심** ``` await ``` 키워드는 async 키워드가 붙은 메소드에서만 사용할 수 있다. 

- 성공 처리 예시
``` js
async function hello() {
  return 'Hello';
}

async function callHello() {
  // 새로 추가된 try 키워드
  try {
    const r = await hello();
    console.log('성공: ' + r);
  } catch (e) {
    console.log('실패: ' + e.message);
   }
}

callHello();

<결과>
# 시작
성공: Hello
# 끝
```

``` js
function promise() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve('resolved');
    }, 2000);
  });
}

async function asyncCall() {
  try {
      console.log(1);
      const result = await promise(); // Promise가 settled될 때까지 기다린 후 resolve된 값을 할당한다.
      console.log(result);
      console.log(2);
  } catch(err) {
    console.error(err); // error 발생 시 catch 블락에서 잡히도록 handling
  }
}

asyncCall();

// 출력 값
1  // asyncCall 호출
resolved  // resolve 함수 호출
2  // await 후 다음 코드 실행
 
그렇다면 아래의 경우 출력 값은 어떠할까

console.log(0);

function promise() {
  console.log(1);
  
  return new Promise(resolve => {
    setTimeout(() => {
      
      console.log(2);
      resolve('resolved');
    }, 2000);
  });
}

console.log(3);

async function asyncCall() {
  try {
      console.log(4);
    
      const result = await promise(); // Promise가 settled될 때까지 기다린 후 resolve된 값을 할당한다.
    
      console.log(result); 
      console.log(5);
  } catch(err) {
    console.error(err); // error 발생 시 catch 블락에서 잡히도록 handling
  }
}

console.log(6);

asyncCall();

< 결과 >
0
3
6
4  // asyncCall 호출
1  // promise 함수 호출
2  // 2초 후 setTimeout 콜백 함수 호출
resolved // resolve함수 호출
5  // await 후 다음 코드 실행
```

- 실패 처리 예시
``` js
async function hello() {
  throw new Error(`Fail!`);
}

async function callHello() {
  try {
    const r = await hello();
    console.log(r);
    // 새로 추가된 catch 키워드
  } catch (e) {
    console.log(e.message);
   }
}

callHello();

<결과>
# 시작
실패: Fail!
# 끝
```

기존 ```then```과 ```catch```는 각각 ``` try-catch ```로 바뀌었다.    
await를 붙인 메소드의 결과가 **성공**일 경우는 **try** 부분이 실행되고 **실패**일 경우는 **catch** 부분이 실행된다.
