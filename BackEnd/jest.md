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