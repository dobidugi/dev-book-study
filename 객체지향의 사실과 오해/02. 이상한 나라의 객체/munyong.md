## ✨ 내용 요약

인간은 선천적으로 타고난 인지 능력을 이용해 세상에 존재하는 다양한 객체를 식별하고 분류함으로써 세상을 이해한다. 객체지향은 이러한 기본적인 인지 능력에 기반을 두고 있다. 인간의 인지 능력은 물리적인 한계를 넘어 추상적인 사물까지도 객체로 인식할 수 있게 한다.

- 소프트웨어에서의 객체: 실세계의 객체와는 다른 모습을 가지며, 객체는 상태, 행동, 식별자를 가진 실체로 표현된다.

### 1. 상태

상태를 알면 행동의 결과를 예측할 수 있다.
ex) 앨리스 키와 문의 높이 > 문 통과 여부

또한, 객체는 다른 객체의 상태를 표현하는 데 사용될 수 있다.
ex) 앨리스라는 객체, 음료라는 객체

### 2. 행동

상태를 이용하여 객체의 행동을 표현할 수 있다.
ex) 앨리스 키가 40센티 이하면 문을 통과할 수 있다.

행동 결과는 다음 두 가지 관점에서 설명된다:

1. 객체 자신의 상태를 변경한다.
2. 협력하는 다른 객체에 메시지를 전송한다.

### 3. 식별자

객체는 단순한 값과 다르게 상태를 변경하고, 시간에 따라 다른 상태를 가질 수 있다. 그럼에도 불구하고 객체는 유일하게 식별 가능하다.

### 상태 캡슐화

객체의 상태를 캡슐화함으로써 객체의 자율성을 높이고 협력을 단순하고 유연하게 만들 수 있다.

### 행동 중심 설계

행동이 상태를 결정하므로, 객체 설계에서 상태보다는 행동에 초점을 맞추는 것이 중요하다.

### 객체지향의 목적

현실을 모방하는 것이 아니라, 소프트웨어에서 창조한 객체의 특성을 활용하여 현실 속 객체 이름을 이용해 객체를 묘사하는 것이다.

## 📝 감상 및 리뷰

- 이상한 나라의 앨리스 이야기에 비유해서 설명한 부분이 인상깊었다.
- 객체와 객체를 표현하는 상태, 행동, 식별자의 관계를 비유를 통해 쉽게 이해할 수 있었다.

## 🛠️ 실무/프로젝트 적용

- 시스템을 설계할 때 단순한 값과 객체의 차이점을 명확하게 구분하고 명시적으로 표현하는 것이 매우 중요하다.
- 행동이 상태를 결정하기 때문에 상태가 아니라 행동에 초점을 맞춰서 객체를 설계하자.
- 상태를 캡슐화하여 객체 간의 협력을
  유연하게 만드는 방식을 적용해보자.

## 🔍 추가 자료

- 더 알아보고 싶은 내용: 상태 캡슐화와 관련된 다양한 설계 패턴에 대해 더 깊이 공부해보고 싶다.
