### XML vs JSON

#### XML (Extensible Markup Language))
다른 특수한 목적을 갖는 마크업 언어를 만드는데 사용하도록 권장하는 다목적 마크업 언어   
``` 마크업 언어 ``` : 태그 등을 이용하여 문서나 데이터의 구조를 명기하는 언어의 한 가지 

#### XMl 의 특징
- 다른 시스템끼리 다양한 종류의 데이터를 손쉽게 교환할 수 있도록 해준다.
- 새로운 태그를 만들어 추가해도 계속해서 동작하므로, 확장성이 좋다.
- 데이터를 보여주지 않고, 데이터를 전달하고 저장하는 것만을 목적으로 한다.
- 텍스트 데이터 형식의 언어로 모든 XML 문서는 유니코드 문자로만 이루어진다. 

XMl 문법
``` xml
<?xml version="1.0" encoding="UTF-8"?>
<shop city="서울" type="마트">
    <food>
        <name>귤</name>
        <sort>과일</sort>
        <cost>3000</cost>
    </food>
    <food>
        <name>상추</name>
        <sort>야채</sort>
        <cost>2000</cost>
    </food>
</shop>
```

#### JSON (JavaScript Object Notation)
데이터를 저장하거나 전송할 때 많이 사용되는 ** 경량의 DATA 교환** 형식   
또는, avascript에서 객체를 만들 때 사용하는 표현식    

#### JSON의 특징
- 서버와 클라이언트 간의 교류에서 일반적으로 많이 사용된다.
- 자바스크립트 객체 표기법과 아주 유사하다.
- 자바스크립트를 이용하여 JSON 형식의 문서를 쉽게 자바스크립트 객체로 변환할 수 있는 이점이 있다.
- JSON 문서 형식은 자바스크립트 객체의 형식을 기반으로 만들어졌다.
- 자바스크립트의 문법과 굉장히 유사하지만 텍스트 형식일 뿐이다.
- 다른 프로그래밍 언어를 이용해서도 쉽게 만들 수 있다.
- 특정 언어에 종속되지 않으며, 대부분의 프로그래밍 언어에서 JSON 포맷의 데이터를 핸들링 할 수 있는 라이브러리를 제공한다.

### JSON 문법
- 태그로 표현하기 보다는 중괄호 ({})같은 형식으로 하고, 값을 ','로 나열   
=> name-value 형식의 쌍 : { String key : String value }
- JSON 형식에서는 null, number, string, array, object, boolean을 사용
``` 
{
  "firstName": "Baek",
  "lastName": "Dami",
  "email": "100damii@gmail.com"
}
```

### JSON 의 문제점
AJAX 는 단순히 데이터만이 아니라 JavaScript 그 자체도 전달할 수 있다.   
JSON 데이터 라고 해서 받았는데 단순 데이터가 아니라 JavaScript가 될 수도 있고, 그게 실행 될 수 있다는 것이다. (데이터인 줄 알고 받았는데 악성 스크립트가 될 수 있음!)    
그래서 순수하게 데이터만 추출하기 위한 JSON 관련 라이브러리를 따로 사용하기도 한다.

### JSON이 가져올 수 있는 데이터
해당 자바스크립트가 로드된 서버의 데이터에만 한정   

예를 들어, http://dmai.kr/json.js에서 불러올 수 있는 데이터는 dami.kr 서버에 존재하는 것만 가능하다. (구글 데이터를 불러온다거나 네이버 데이터를 불러온다거나 할 수 없다.)   
JSON은 단순히 데이터 포맷일 뿐이며 그 데이터를 불러오기 위해선 XMLHttpRequest()라는 JavaScript 함수를 사용해야 하는데 이 함수가 동일 서버에 대한 것만 지원하기 때문이다. 

### JSON 형식 텍스트를 JavaScript Object로 변환하기
```
var jsonText = '{ "name": "Dami ", "lastName": "Baek" }';  // JSON 형식의 문자열
var realObject = JSON.parse(jsonText);
var jsonText2 = JSON.stringify(realObject);

console.log(realObject);
console.log(jsonText2);
```
**JSON.parse( JSON으로 변환할 문자열 )** : JSON 형식의 텍스트를 자바스크립트 객체로 변환한다.
**JSON.stringify( JSON 문자열로 변환할 값 )** : 자바스크립트 객체를 JSON 텍스트로 변환한다.