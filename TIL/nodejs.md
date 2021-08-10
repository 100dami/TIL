## < Java Script >    

### Promise가 뭐지?
> 자바스크립트 ```비동기 처리```에 사용되는 객체 <br>
##### 여기서 비동기 처리란, ‘특정 코드의 실행이 완료될 때까지 기다리지 않고 다음 코드를 먼저 수행하는 자바스크립트의 특성’

### Promise가 왜 필요할까?
> 프로미스는 주로 서버에서 받아온 데이터를 화면에 표시할 때 사용하는데,    
이 때 데이터를 다 받아오기도 전에 데이터를 화면에 표시하려고 하면 오류가 발생하거나 빈 화면이 뜬다.    
그래서 이 문제점을 해결하고자 Promise 를 사용하는 것임!

#### 프로미스를 사용한 코드 예시
``` js 
function getData(callback) {
  // new Promise() 추가
  return new Promise(function(resolve, reject) {
    $.get('url 주소/products/1', function(response) {
      // 데이터를 받으면 resolve() 호출
      resolve(response);
    });
  });
}

// getData()의 실행이 끝나면 호출되는 then()
getData().then(function(tableData) {
  // resolve()의 결과 값이 여기로 전달됨
  console.log(tableData); // $.get()의 reponse 값이 tableData에 전달됨
});
```
