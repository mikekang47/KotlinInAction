### 코틀린의 주요 특성

1. 대상 플랫폼: 서버, 안드로이드 등 자바가 실행되는 모든 곳.
2. 정적 타입 지정 언어
3. 함수형 프로그래밍과 객체지향 프로그래밍
4. 무로 요픈소스

---

코틀린의 대상 플랫폼은 자바가 실행되는 모든 곳이기 때문에 플랫폼 제약이 적다.
특히 코틀린 1.1부터는(현재는 1.7) 자바스크립트 빌드를 공식적으로 지원하기 때문에 훨씬 사용성이 올라갔다.



코틀린은 정적 타입 지정 언어이기 때문에 컴파일 시에 타입에 대한 검증이 일어난다.(컴파일타임 검증)
타입 지정 덕분에 성능, 신뢰성, 유지 보수성, 도구 지원 등에서 장점이 있다.
하지만 코틀린의 타입 추론 덕분에 모든 곳에 타입을 명시할 필요는 없다. (다만 명시하면 빌드 속도는 월등히 빨라진다.)
코틀린은 다른 언어들과는 다르게 널이 될 수 있는 타입을 지원한다. 즉, NP를 미리 감지할 수 있다.


코틀린은 객체지향 언어인 동시에 함수형 언어다.
함수를 변수에 저장할 수 있으며, 함수를 인자로 다른 함수에 전달할 수 있다.
불변성의 특징도 가지기에 값 객체로서의 프로그래밍에 용이하다.
함수형 스타일로 코드를 작성하면 간결성, thread-safe, 테스트 용이성의 장점을 가진다.



