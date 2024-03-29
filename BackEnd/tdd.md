## TDD (Test Driven Development)
테스트 주도 개발 : 즉, 테스트가 개발을 이끌어 나간다.      
소프트웨어를 개발하는 여러 방법론 중 하나    
[Jest](./jest.md) <- JS 테스트 프레임워크

### TDD 의 프로세스
제품이 오류 없이 정상 작동하는지 확인하기 위해 모든 코드는 프로그래머가 작성하고 나서 테스트를 거치게 되는데, ```TDD``` 에서는 제품의 기능 구현을 위한 코드와 별개로, 해당 기능이 정상적으로 움직이는지 검증하기 위한 테스트 코드를 작성한다.     
테스트가 실패할 경우, 테스트를 통과하기 위한 최소한으로 코드를 개선한다.      
최종적으로 테스트에 성공한 코드를 리팩토링 한다.

### 추상적인 레벨에서의 TDD의 핵심 개념
결정과 피드백 사이의 갭에 대한 인식, 결정과 피드백 사이의 갭을 조절하기 위한 테크닉   
```
결정: 1 을 목표로 코드를 작성할 때, ‘나는 빼기로 나이를 구해야겠다.’라는 것을 결정한다.
피드백: 빼기로 계산했을 때의 코드를 테스트 프로그램을 실행한 결과로, 된다/안된다라는 프로그램 상의 피드백을 받는다.
이 둘 사이의 갭을 내가 인식한다면 TDD를 하고 있는 것이다.
```

### TDD 의 장점
- 설계 수정 시간 단축
- 디버깅 및 버그 수정 시간 단축
- 문제 발생 시 모듈별 테스트를 통해 문제 지점을 빠르게 파악 가능
P- roduction 레벨에서 버그를 수정하는 것은 Software development lifecycle (SDLC)에서 버그를 수정하는 것보다 훨씬 큰 비용과 시간을 소모
- Refactoring을 통해 Clean code를 유지
- 객체지향적인 코드 개발
- 세부 비즈니스 로직을 객체 내부로 숨겨 변경에 대응
- 유지보수 및 재사용에 용이

### TDD 의 필요성
애자일에서 설명한 것과 같이 불확실성이 높을 때 ‘피드백’과 ‘협력’이 중요하다.     
** 피드백과 협력이 중요한 이유**
- 불확실성이 높을 때 ‘피드백’과 ‘협력’을 이용하면 더 좋은 결과가 나올 확률이 높아진다.
- TDD도 마찬가지로 ‘피드백’과 ‘협력’을 증진시키는 것이기 때문에 불확실성이 높을 때 도움이 되는 것이다.

