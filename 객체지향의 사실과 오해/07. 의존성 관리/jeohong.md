# 07. 함께 모으기

리뷰기간: 2024년 11월 25일 → 2024년 12월 1일
태그: 작성중

## ✨ 내용 요약

- 객체지향의 세가지 관점
    - 개념 관점 : 설계는 도메인 안에 존재하는 개념과 개념들 사이의 관계 표현
        - 도메인 : 사용자들이 관심을 가지고 있는 특정 분야나 주제
        - 소프트웨어 : 도메인에 존재하는 문제를 해결하기 위해 개발
    - 명세 관점 : 실제 소프트웨어 안에서 살아 숨쉬는 객체들의 책임에 초점
        - 프로그래머는 객체가 협력을 위해 `무엇` 을 할 수 있는지에 대한 초점
        - 인터페이스와 구현을 분리하는 것은 훌륭한 객체지향 설계의 기본원칙
    - 구현 관점 : 실제 작업을 수행하는 코드와의 연관
        - 객체들이 책임을 수행하는데 필요한 동작하는 코드를 작성
        - 프로그래머는 객체의 책임을 어떻게 수행할지에 대한 초점
        - 인터페이스를 구현하는데 필요한 `속성`과 `메서드`를 클래스에 추가
    - 세 관점은 동일한 클래스를 세가지 다른 방향에서 바라보는것을 의미
        - 클래스가 은유하는 개념은 도메인 관점을 반영
        - 클래스의 공용 인터페이스는 명세 관점을 반영
        - 클래스의 속성과 메서드는 구현 관점을 반영
- 커피전문점 도메인으로 바라본 실제 구현 ( Swift 변환 )
    - 인터페이스 정리하기
        
        ```swift
        class Customer {
        	public func order(menuName: String) { }
        }
        
        class MunuItem { }
        
        class Menu {
        	public func choose(name: String) -> MenuItem { }
        }
        
        class Barista {
            public func makeCoffee(menuItem: MenuItem) -> Coffee { }
        }
        
        class Coffee {
            public func Coffee(menuItem: MenuItem) { }
        }
        
        class Customer {
            func order(menuName: String) { }
        }
        
        class MenuItem { }
        
        class Menu {
            func choose(name: String) -> MenuItem {
                return MenuItem()
            }
        }
        
        class Barista {
            func makeCoffee(menuItem: MenuItem) -> Coffee {
                return Coffee(menuItem: menuItem)
            }
        }
        
        class Coffee {
            init(menuItem: MenuItem) { }
        }
        ```
        
    - 구현 하기
        
        ```swift
        // Customer
        class Customer {
            func order(menuName: String, menu: Menu, barista: Barista) {
                let menuItem = menu.choose(name: menuName)
                let coffee = barista.makeCoffee(menuItem: menuItem)
            }
        }
        
        // Menu
        class Menu {
            private var items: [MenuItem]
        
            init(items: [MenuItem]) {
                self.items = items
            }
        
            func choose(name: String) -> MenuItem? {
                for item in items {
                    if item.getName() == name {
                        return item
                    }
                }
                return nil
            }
        }
        
        // Barista
        class Barista {
            func makeCoffee(menuItem: MenuItem) -> Coffee {
                let coffee = Coffee(menuItem: menuItem)
                return coffee
            }
        }
        
        // Coffee
        class Coffee {
            private var name: String
            private var price: Int
        
            init(menuItem: MenuItem) {
                self.name = menuItem.getName()
                self.price = menuItem.cost()
            }
        }
        
        // MenuItem
        class MenuItem {
            private var name: String
            private var price: Int
        
            init(name: String, price: Int) {
                self.name = name
                self.price = price
            }
        
            func cost() -> Int {
                return price
            }
        
            func getName() -> String {
                return name
            }
        }
        
        ```
        
- 코드와 세가지 관점
    - 코드는 세가지 관점을 모두 제공해야 한다
    - 개념 관점
        - 개념 관점에서의 예시 코드 **`Customer, Menu, MenuItem, Barista, Coffee 클래스`**
        - 이 클래스들을 살펴보면 **`커피 전문점 도메인을 구성하는 중요한 개념과 관계를 반영`**
        - 소프트웨어 클래스가 도메인 개념의 특성을 최대한 수용하면 **`변경을 관리하기 쉽고 유지보수성을 향상`**
        - 커피를 제조하는 과정을 변경해야 한다면 Barista 클래스가 커피를 제조할 것이라고 쉽게 유추
    - 명세 관점
        - 명세 관점은 **클래스의 인터페이스**를 바라봄
        - 클래스의 public 메서드는 다른 클래스가 협력할 수 있는 공용 인터페이스 (Swift에서는 아무표시도 없는 것을 의미 ( 기본값 ) )
        - 공용 인터페이스는 외부의 객체가 해당 객체에 접근할 수 있는 유일한 부분
        - 최대한 변화에 안정적인 인터페이스를 만들기 위해서는 **`인터페이스를 통해 구현과 관련된 세부 사항이 드러나지 않게 해야 함`**
    - 구현 관점
        - 구현 관점은 클래스의 내부 구현을 바라본다
        - 클래스의 **메서드와 속성**은 구현에 속하며 공용 인터페이스의 일부가 아님
        - 메서드의 구현과 속성의 변경은 원칙적으로 외부의 객체에게 영향을 미쳐서는 안됨
        - 이것은 메서드와 속성이 철저하게 **`클래스 내부로 캡슐화돼야 한다는 것을 의미`**
- 인터페이스와 구현을 분리하라
    - 인터페이스가 구현 세부 사항을 노출하기 시작하면 아주 작은 변동에도 전체 협력이 요동치는 취약한 설계를 얻을 수 밖에 없음
    - 실제로 훌륭한 설계를 결정하는 측면은 명세 관점은 객체의 인터페이스
    - 명세 관점이 설계를 주도하게 하면 설계의 품질이 향상
    - 중요한 것은 클래스를 봤을 때 클래스를 명세 관점과 구현 관점으로 나눠볼 수 있어야한다
    - 캡슐화를 위반해서 구현을 인터페이스 밖으로 노출해서도 안되고, 인터페이스와 구현을 명확하게 분리하지 않고 흐릿하게 섞어놓아서도 안된다

## 📝 감상 및 리뷰

- 책에 처음으로 코드가 등장하여 이를 나의 주력 언어인 Swift로 바꿔보며 좀더 쉽게 이해 할 수 있었음
- 인터페이스와 구현의 분리를 좀더 명확하게 해야겠다고 느낌

## 🛠️ 실무/프로젝트 적용

- 인터페이스와 구현의 분리에 신경을 써야함
- 세가지 관점에 대해 생각하며 코드를 작성할 것