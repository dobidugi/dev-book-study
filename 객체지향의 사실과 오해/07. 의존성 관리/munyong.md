## ✨ 내용 요약

마틴 파울러가 설명하는 객체지향 설계의 세 가지 상호 연관된 관점

#### 1. 개념 관점

- 도메인 내의 중요한 개념과 개념 사이의 관계를 반영하는 관점.
- 사용자 관점에서 도메인을 바라보며, 실제 도메인의 규칙과 제약을 최대한 유사하게 모델링.
- 도메인의 예: 커피 전문점
  - 타입 분류: 손님, 메뉴판, 메뉴 항목, 바리스타, 커피
  - 관계: 포함 관계(합성 관계), 연관 관계(관계 유무가 중요)

#### 2. 명세 관점

- 객체의 책임과 인터페이스에 초점을 맞춘 관점.
- "무엇을 할 수 있는지"를 인터페이스를 통해 정의하며, 구현과 인터페이스의 분리를 중시.
  - 인터페이스는 외부에서 객체에 접근할 수 있는 유일한 진입점.
  - 인터페이스를 통해 구현 세부 사항이 노출되지 않도록 설계.
- 설계 시 협력(메시지 전달)을 기반으로 객체의 인터페이스 구성:
  ```Java
  class Customer {
    public void order(String menuName, Menu menu, Barista barista) {
      MenuItem menuItem = menu.choose(menuName);
      Coffee coffee = barista.makeCoffee(menuItem);
    }
  }
  ```

#### 3. 구현 관점

- 객체의 책임을 수행하기 위한 구체적인 동작을 코드로 작성하는 관점.
- 메서드와 속성을 클래스 내부로 캡슐화하여 외부에서 접근할 수 없도록 해야 함.
- 구현 도중 객체의 인터페이스가 변경될 수 있음.

  ```Java
  class Coffee {
    private String name;
    private int price;

    public Coffee(MenuItem menuItem) {
      this.name = menuItem.getName();
      this.price = menuItem.cost();
    }
  }
  ```

### 설계 및 구현 과정

#### 1. 도메인 모델 설계

- 도메인의 타입과 관계를 정의.
- 예: 커피 전문점 도메인에서 손님, 메뉴, 바리스타, 커피 타입 분류.

#### 2. 협력 기반 설계

- 메시지(행위)를 먼저 정의하고 이를 기반으로 객체의 인터페이스 구성.

#### 3. 구현 단계

- 설계를 바탕으로 객체의 동작을 메서드로 작성.
- 설계 후 빠르게 구현에 돌입하며 필요시 인터페이스를 수정.

### 세 가지 관점의 중요성

- 개념 관점: 도메인의 중요한 개념과 관계를 모델링.
- 명세 관점: 객체 간 협력과 인터페이스 설계.
- 구현 관점: 책임 수행을 위한 구체적인 코드 작성.
- 설계의 핵심: 명확한 관점 분리와 인터페이스-구현 분리.
  - 명세 관점이 설계를 주도할 경우 설계 품질이 향상됨.
  - 클래스를 명세와 구현 관점으로 나눠볼 수 있도록 설계 개선.

## JavaScript 코드 예제: 커피 전문점

```JavaScript
class Customer {
  order(menuName, menu, barista) {
    const menuItem = menu.choose(menuName);
    if (!menuItem) {
      console.error(`${menuName}은(는) 메뉴에 없습니다.`);
      return;
    }
    const coffee = barista.makeCoffee(menuItem);
    console.log(`${menuName} 주문이 완료되었습니다:`, coffee);
  }
}

class Menu {
  constructor(items) {
    this.items = items;
  }

  choose(name) {
    return this.items.find(item => item.name === name) || null;
  }
}

class Barista {
  makeCoffee(menuItem) {
    return new Coffee(menuItem);
  }
}

class Coffee {
  constructor(menuItem) {
    this.name = menuItem.name;
    this.price = menuItem.price;
  }
}

class MenuItem {
  constructor(name, price) {
    this.name = name;
    this.price = price;
  }

  cost() {
    return this.price;
  }
}

// 사용 예제
const americano = new MenuItem("아메리카노", 4000);
const latte = new MenuItem("카페라떼", 4500);

const menu = new Menu([americano, latte]);
const barista = new Barista();
const customer = new Customer();

customer.order("아메리카노", menu, barista); // 정상 주문
customer.order("에스프레소", menu, barista); // 없는 메뉴 처리
```

## 📝 감상 및 리뷰

- 실제 구현까지의 과정을 코드 예제를 통해 구체적으로 알게 되었다.
- 단순히 이론적으로 개념 관점, 명세 관점, 구현 관점을 나누는 것이 아니라, 이를 바탕으로 객체 간의 협력과 메시지 중심 설계가 어떻게 이루어지는지 더 명확히 이해할 수 있었다.

## 🛠️ 실무/프로젝트 적용

앞으로 프로젝트 설계 시, 개념 관점에서 도메인을 먼저 모델링하고, 명세 관점에서 인터페이스 중심의 설계를 진행한 뒤, 구현 관점으로 동작을 구체화하는 접근 방식을 사용할 계획이다.

## 🔍 추가 자료

- 더 알아보고 싶은 자료는 없지만, 이 내용을 기반으로 '객체지향 설계 원칙(SOLID)'과 추가로 마틴 파울러의 책 Refactoring도 참고해 보면 좋을 듯하다.
