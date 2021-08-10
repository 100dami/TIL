## 노드의 Fs 시스템

### 비동기식을 사용한 예시 코드!
``` js
const fs = require('fs');

console.log('시작');
fs.readFile('./test2.txt', (err, data) => {
    if(err) {
        throw(err);
    };
    console.log('1번', data.toString());
});
fs.readFile('./test2.txt', (err, data) => {
    if(err) {
        throw(err);
    };
    console.log('2번', data.toString());
});
fs.readFile('./test2.txt', (err, data) => {
    if(err) {
        throw(err);
    };
    console.log('3번', data.toString());
});
console.log('끝');
```
콘솔 창 결과
```
시작
끝
2번 저를 여러번 읽어 보세요 ~
1번 저를 여러번 읽어 보세요 ~
3번 저를 여러번 읽어 보세요 ~
```
시작, 끝의 순서만 같을 뿐 나머지는 순서가 랜덤하게 나오는데, 그 이유는!    

비동기 메서드들은 백그라운드에 해당 파일을 읽으라고만 요청하고 다음 작업으로 넘어간다.    
그래서 파일 읽기 요청만 3번 보내고 console에 '끝'을 찍는다.
=> 비동기-논블로킹 방식

### 동기식을 사용한 예시 코드!

``` js
const fs = require('fs');

console.log('시작');
let data = fs.readFileSync('./test2.txt');
console.log('1번', data.toString());
data = fs.readFileSync('./test2.txt');
console.log('2번', data.toString());
data = fs.readFileSync('./test2.txt');
console.log('3번', data.toString());
console.log('끝');
```
콘솔 창 결과
```
시작
1번 저를 여러번 읽어 보세요 ~
2번 저를 여러번 읽어 보세요 ~
3번 저를 여러번 읽어 보세요 ~
끝
```
코드의 쓰임대로 순서대로 결과가 나와서 좋지만, 이런 동기식 코드는 이전 작업이 완료 되어야 다음 작업을 할 수 있기 때문에 매우 비효율 적인 방법임!