### 🎯📝📋📎 var 키워드로 선언한 변수의 문제점

- 변수의 중복 선언 허용
- var 키워드로 선언한 변수는 오직 함수의 코드 블록만을 인정하기에 외부에서 선언한 변수는 내부에서 선언해도 모두 전역 변수가 되는 함수 레벨 스코프
- 변수 호이스팅으로 인한 선참조 가능 => 흐름상 오류, 가독성 저하

### 📝 let 키워드

- 변수 중복 선언 금지

  - var 와는 다르게 중복시 syntaxError

- 블록 레벨 스코프

  - 모든 코드 블록(함수,if문, for문, while문, try/catch문)을 지역 스코프로 인정하는 블록 레벨 스코프

- 변수 호이스팅

  - var와는 다르게 선언 단계, 초기화 단계가 분리되어서 진행
  - 스코프의 시작 지점부터 초기화 시작 지점까지 변수를 참조할 수 없는 일시적 사각지대(TDZ)덕에 호이스팅이 발생하지 않는 것처럼 동작

- 전역 객체와 let
  - let 키워드로 선언한 전역 변수는 전역 객체의 프로퍼티가 아니기에, window.변수명 같이 접근이 불가능하다.
  - 보이지 않는 개념적인 블록(전역 렉시컬 환경의 선언적 환경 레코드) 내에 존재한다.

### 📝 const 키워드

대부분 상수(재할당이 금지된 변수)를 선언하기 위해 사용하며 let 과 특징이 대부분 동일하다.

let 과 다른점

- 선언과 초기화

  - 반드시 선언과 동시에 초기화 해야한다.

- 재할당 금지

- 상수

  - const에 원시값을 할당할 경우 값을 변경할 수 없기에 상수로 표현하는데 사용한다.
  - 상태유지, 가독성, 유지보수의 편의를 위해 적극적으로 사용해야 한다.
  - 대문자와 언더스코어로 구분하여 스네이크 케이스로 표현하는 것이 일반적이다.

- const 키워드와 객체
  - const 키워드에 객체를 할당한 경우 객체는변경 가능한 값이므로 값을 변경할 수 있다.
  - const 키워드는 재할당을 금지할 뿐, "불변"을 의미하진 않는다.

### 📝 var vs let vs const

기본적으로 const를 사용하고 재할당이 필요한 경우 let 을 사용하는 것이 좋다.

- ES6를 사용한다면 var는 사용하지 않는다.
- 재할당이 필요한 경우를 한정해 let을 사용하되, 스코프를 최대한 좁게 만든다.
- 변경이 발생하지 않는 읽기 전용의 원시값과 객체에는 재할당이 금지되는 const를 안전하게 사용한다.

> 일단 const로 작성하고 필요한 경우 let으로 변경해도 결코 늦지 않다.
