## Promise


### Promise가 뭐지?
> 자바스크립트 ```비동기 처리```에 사용되는 객체 <br>
##### 여기서 비동기 처리란, ‘특정 코드의 실행이 완료될 때까지 기다리지 않고 다음 코드를 먼저 수행하는 자바스크립트의 특성’

### Promise가 왜 필요할까?
> 프로미스는 주로 서버에서 받아온 데이터를 화면에 표시할 때 사용하는데,    
이 때 데이터를 다 받아오기도 전에 데이터를 화면에 표시하려고 하면 오류가 발생하거나 빈 화면이 뜬다.    
그래서 이 문제점을 해결하고자 Promise 를 사용하는 것임!   
그리고 비동기 호출 시, 마치 동기 호출 처럼 값을 반환할 수 있다!

### Promise 의 상태
- 대기(pending): 이행하거나 거부되지 않은 초기 상태
- 이행(fulfilled): 연산이 성공적으로 완료됨
- 거부(rejected): 연산이 실패함

### Promise 의 사용 방법
``` js 
new Promise(function(resolve, reject) {
  // ...
});
```
```resolve```는 결과가 성공인 Promise 객체를 반환, ```reject```는 결과가 실패인 Promise 객체를 반환    
반환된 Promise 객체를 처리할 때 성공 시 ```then```을 사용하고 실패 시 ```catch```를 사용하여 처리

### 프로미스를 사용한 코드 예시
- 성공 예시
``` js 
let myFirstPromise = new Promise((resolve, reject) => {
  setTimeout(function(){
    // 성공 시 resolve 사용
    resolve(`Success!`);
  }, 3000);
});

// 성공 시 then 사용하여 결과 처리
myFirstPromise.then((successMessage) => {
  console.log(`Yay! ` + successMessage);
});

<결과>
# 시작
(3초 대기)
Yay! Success!
# 종료
```
- 실패 예시
``` js
let myFirstPromise = new Promise((resolve, reject) => {
  setTimeout(function(){
    // 실패 시 resolve 사용
    reject(new Error(`Fail!`));
  }, 3000);
});

// reject를 사용하여 Promise 객체를 반환하기 때문에 then은 실행되지 않는다.
myFirstPromise.then((successMessage) => {
  console.log(`Yay! ` + successMessage);
})
// 실패 시 catch 사용하여 결과 처리
.catch((reason) => {
  console.log('여기서 거부된 프로미스( ' + reason + ' )를 처리하세요.');
});

<결과>
(3초 대기)
여기서 거부된 프로미스( Error: Fail )를 처리하세요.
```

- 콜백 지옥에서 벗어난 promise 의 코드
``` js
function a() {
  return new Promise({
    // ...
  });
}

function b() {
  return new Promise({
    // ...
  });
}

function c() {
  return new Promise({
    // ...
  });
}

myFirstPromise()
.then(a)
.then(b)
.then(c);
```

