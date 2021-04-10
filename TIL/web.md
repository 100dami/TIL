## Web에 대해 알아보자 🔎 

### HTML? 
> *월드 와이드 웹에 내재된 *프로토콜   

``` 
월드 와이드 웹 (World Wide Web) :
WWW, 또는 웹 이라고 부르는데,
인터넷에 연결된 컴퓨터를 통해 사람들이 정보를 공유할 수 있는 전 세계적인 정보 공간을 뜻 함 

프로토콜 (Protocol) :
컴퓨터나 원거리 통신 장비 사이에서 통신을 원활하게 수용하도록 해주는 통신 규약, 약속
```

### HTTP? 
> HyperText Transfer Protocol의 약자로, WWW상에서 정보를 주고받는 데 사용되는 프로토콜 <br>
주로 HTML 문서를 주고받는 데에 쓰이고, 주로 *TCP를 사용하고 HTTP/3 부터는 *UDP를 사용하며, 80번 *포트를 사용

##### TCP/ UDP 그리고 포트(Port)
![tcpudp](https://user-images.githubusercontent.com/68890057/103987937-959bdf80-51d0-11eb-9a37-df1cb9f7d35b.jpg)
>컴퓨터에서의 포트(port)란 외부의 다른 장비와 접속하기 위한 플러그와 같은 것을 의미

### HTTP 1.1?
전송의 성공과 실패 여부를 알 수 있는 상태 코드가 생겨남 <br>
헤더 개념이 요청과 응답 모두에 도입 됨 <br>
이 헤더(Content-Type)의 도움으로 HTML 뿐만아니라 다른 문서들도 전송 가능해 지게 됨

### HTTP 2?
http 1.0의 속도의 문제점을 개선하여 나온 프로토콜 <br>

### HTTP 1.1 과 HTTP 2의 차이점?
http 1.0 과는 다르게      
* **Multiplexed Streams**(한 커넥션에 여러개의 메세지를 동시에 주고 받을 수 있음)
* **Server Push**(HTML문서상에 필요한 리소스를 클라이언트 요청없이 보내줄 수 있음)
* **Header Compression**(Header 정보를 HPACK압충방식을 이용하여 압축전송) 등의 기술이 쓰임 <br>
![http](https://user-images.githubusercontent.com/68890057/103990667-f4635800-51d4-11eb-99eb-b079dfa888a6.png)


---
### 프레임워크란?
> 어플리케이션을 개발에 필요한 스크립트를 위에서 이야긴 것과 같은 관점에서 정리한 스크립트 모음이라고 할 수 있다. 

### Express 를 사용하는 이유
> 1. 단순함


@copyright google

 