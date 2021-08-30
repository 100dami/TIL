## Jest
**JS 테스트 프레임워크**, 내가 작성한 코드가 제대로 동작하는지 확인할 때 사용     
여러가지 상황들을 설정하고, 그 상황에 맞는 결과가 나오는지 자동으로 테스트 해줌!

### 설치
```
$ npm i -D jest babel-jest @babel/core @babel/preset-env
```
jest와 babel-jest를 함께 설치한다.     
(jest로 테스트할 때 ES6이상의 문법을 사용하기 위해선 babel의 도움이 필요하기 때문)
#### 1. jest.config.js
``` js
module.exports = {
  moduleFileExtensions: ["js", "json", "jsx", "ts", "tsx", "json"],
  transform: {
    "^.+\\.(js|jsx)?$": "babel-jest",
  },
  moduleNameMapper: {
    "^@/(.*)$": "<rootDir>/$1",
    '\\.(jpg|ico|jpeg|png|gif|eot|otf|webp|svg|ttf|woff|woff2|mp4|webm|wav|mp3|m4a|aac|oga)$':
      '<rootDir>/__mocks__/fileMock.js',
    '\\.(css|less)$': '<rootDir>/__mocks__/fileMock.js',
  },
  testMatch: [
    "<rootDir>/**/*.test.(js|jsx|ts|tsx)",
    "<rootDir>/(tests/unit/**/*.spec.(js|jsx|ts|tsx)|**/__tests__/*.(js|jsx|ts|tsx))",
  ],
  transformIgnorePatterns: ["<rootDir>/node_modules/"],
};
```
루트 폴더에 jest.config.js를 만들고 상기 내용을 적는다.       
moduleFileExtensions, moduleNameMapper, testMatch는 테스트를 적용할 파일들을 설정한다.         
moduleNameMapper를 통해 특정 파일명을 가진 리소스들은 fileMock.js로 대체하였다. (이런 처리를 하지 않으면 리소스 때문에 에러가 발생한다.)    
transform은 babel 처리를 설정한다.       
transformIgnorePatterns는 test 제외 대상을 설정한다.

#### 2. fileMock.js
```
module.exports = '';
```
이미지나 음원 파일을 통해 무엇인가 확인하는 일은 없을 것이다.       
의미 없는 빈문자열을 export 하는 것으로 충분하다.

#### 3. babel.config.js
``` js
module.exports = {
  presets: [
    [
      "@babel/preset-env",
      {
        targets: {
          node: "current",
        },
      },
    ],
  ],
};
```
루트 폴더에 babel.config.js를 만들고 상기 내용을 적는다.       
바벨 적용시 preset을 적용할 수 있도록 설정한다.

#### 4. package.json
``` 
"scripts": {
    "test": "jest",
  },
```
package.json에 test 실행시 jest가 실행되도록 작성한다.     

### Test 파일 작성 규칙
```테스트파일이름.test.js``` 로 파일을 작성하거나
```__tests__``` 폴더에 들어있는 test 파일들은 일괄적으로 테스트된다

### 테스트 방법
#### 1. 기초 문법
``` js
let temp;
describe("simple test", () => {
  beforeEach(() => {
    temp = 1;
  });
  
  afterEach(() => {
    temp = 0;
  });
  
  test('1 is 1', () => {
    expect(1).toBe(1);
  });
  
  test('[1,2,3] is [1,2,3]', () => {
    expect([1,2,3]).toEqual(1);
  });
})
```
##### describe
테스트 단위를 묶는 가장 큰 단위, 테스트 시 describe에 설명된 내용으로 테스트 단위를 크게 분류 해준다.

##### test, it
test(), it()을 통해 기본 테스트를 한다.
test와 it의 기능적 차이는 없지만 it의 경우 다른 테스트 프레임워크에서 많이 사용하기 때문에 넣은 것이다.

##### expect
expect()안에 테스트할 변수나 값을 넣고, toBe나 toEqual을 이용해 예측 값과 비교한다.

##### toBe, toEqual
결과 예측으로 가장 많이 쓰는 문법은 toBe와 toEqual      
toBe는 단순 비교, toEqual은 배열이나 객체 내부까지 깊은 비교를 해준다.    

##### beforeEach, afterEach
``` js
let temp;
describe("simple test", () => {
  beforeEach(() => {
    temp = 1;
  });
  
  afterEach(() => {
    temp = 0;
  });
  
  test('tmep is 1', () => {
    expect(temp).toBe(1); // true
  });
  
  test('temp is 1', () => {
    expect(temp).toBe(1); // true
  });
});
```
**beforeEach** 는 test()가 실행할 때마다 실행해주는 전처리기       
**afterEach**의 경우 test()가 종료될 때마다 실행하는 후처리기     
따라서 위 예시에서 몇번의 테스트를 하더라도 temp는 1이 된다.

#### 2. Mock 함수를 만들어 테스트
비동기 함수, 특히 API를 Call하는 함수를 테스트할 때 백엔드 서버의 상황에 따라 테스트 결과가 달라질 수 있다는 문제가 있다.      
이러한 문제를 **Mock 함수** 로 해결할 수 있다.       
jest 환경에서는 fetch와 같은 함수를 제공하지 않는다.       
따라서 fetch를 임의로 만들어주면 테스트 환경에서의 fetch는 내가 만든 가짜 fetch가 실행된다.     
(axios의 경우에도 일단 axios를 import 후 임의로 axios 함수를 만들어 줄 수 있다)
```
fetch : api를 불러오고, Promise 객체로 정보를 내보내주는 함수
axios : 브라우저, Node.js를 위한 Promise API를 활용하는 HTTP 비동기 통신 라이브러리
```
##### 예시 코드
``` js
import CommentModel from "../js/model/CommentModel";

test("데이터가 없을 경우 빈배열 리턴", async () => {
  beforeEach(() => {
    commentModel = new CommentModel();
  });
  
  global.fetch = jest.fn().mockImplementation(() => {
    return new Promise((resolve, reject) => {
      resolve({
        json: () => {
          return [];  // 빈배열 리턴
        },
      });
    });
  });

  const comments = await commentModel.getComments(1);
  expect(comments.length).toBe(0); // 리턴 값이 빈배열인지 확인
});
```
commentModel안의 getComments()가 fetch 함수를 사용한다고 가정하자.     
jest test환경 안에서 fetch를 임의의 함수로 만들어 줬기 때문에 getComments에서 fetch를 호출하더라도 내가 임의로 만든 목함수가 호출된다.    
따라서 fetch 호출시 백엔드 API와 상관없이 빈배열을 리턴하도록 만들 수 있다.        

만약 기존에 사용하는 라이브러리를 import해서 사용할 때 ```jest.mock``` 을 사용하여 해결할 수 있다.

``` js
jest.mock('electron', () => ({
  ipcRenderer: { invoke: jest.fn(), on: jest.fn() },
}));
```
 electron의 ipc통신 함수를 mock 함수로 만들고 싶을 땐,   
위와 같이 mock을 생성한 후 대신 리턴할 객체를 가진 함수를 넣어주면 된다.

#### 4. 뷰테스트


