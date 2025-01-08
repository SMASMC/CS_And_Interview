# 디자인 패턴
디자인 패턴이란?
개발을 진행하면서 발생하는 반복적인 문제들을 어떻게 해결할 것인지에 대한 해결방안 중 하나이다. 즉, 소프트웨어 개발에서 자주 발생하는 문제를 해결하기 위해 반복적으로 사용할 수 있는 <span style=color:gold>재사용 가능한 해결책</span>이라고 볼 수 있다.
단지 코드만 '재사용'하는 것이 아니라 더 큰 그림을 그리기 위한 디자인 또한 재사용이 가능하다.
![](https://velog.velcdn.com/images/king33/post/330a11ba-7491-4e62-8de8-fffb4119b259/image.png)


## 🎇 장점
효율적인 문제 해결 - 이미 검증된 방법을 사용하여 문제를 빠르게 해결할 수 있음.
코드 가독성 및 유지보수성 향상 - 코드 구조가 명확해지고 협업 시 의사소통이 쉬워짐.
확장성과 유연성 - 요구사항 변경에 더 쉽게 대응할 수 있음.

## 범주
범주로는 디자인 패턴 용도에 따라 크게 3가지 정도로 나뉜다.
>
* 생성 패턴 - 싱글톤 / 추상 팩토리 / 팩토리 메소드
* 행동 패턴 - 템플릿 메소드 / 상태 / 반복자
* 구조 패턴 - 데코레이터 / 프록시 / 컴포지트

각 용도마다 크게 3가지 정도만 간단하게 알아보자.

---
# <span style=color:green>생성 패턴
"객체 생성과 관련된 패턴으로, 객체 생성의 복잡성을 숨기고, 코드의 유연성을 높여준다"
## 1. 싱글톤 패턴
![](https://velog.velcdn.com/images/king33/post/6b1c54a9-5624-43ca-b471-5660d4c636bb/image.PNG)

싱글톤(Singleton) 패턴의 정의는 아주 간단하다. 객체의 인스턴스가 오직 1개만 생성되는 패턴을 의미한다.
-> [딱 하나만 있어야 하는 객체를 보장하는 패턴]

Q. <span style=color:skyblue>언제 사용하는가?</span>
프로그램에서 오직 하나의 객체만 있어야 할 때 (ex - 설정관리, DB연결)
Q. <span style=color:skyblue>어떻게 작동하는가?</span>
클래스가 자기 자신을 관리하여 딱 한 번만 객체를 생성하고, 생성된 객체를 어디에서든 접근 가능하도록 만든다.
Q. <span style=color:skyblue>싱글톤 패턴을 아주 쉽게 비유하자면?</span>
집에 한 대만 있는 냉장고로 비유할 수 있다. 여러 사람이 있더라도 냉장고는 한 대면 충분하다.

이제 코드로서 싱글톤의 모습을 살펴보자.
```
class Singleton {
  constructor() {
    if (Singleton.instance) {
      return Singleton.instance; // 이미 인스턴스가 존재하면 반환
    }
    Singleton.instance = this; // 새로운 인스턴스를 저장
  }

  someMethod() {
    console.log("싱글톤 메서드 호출!");
  }
}

// 사용 예시
const instance1 = new Singleton();
const instance2 = new Singleton();

console.log(instance1 === instance2); // true (같은 인스턴스 일 때)
```
이를 보고 알 수 있는 것들
<특징>
1. 객체 자체에는 접근이 불가능하다.
2. 객체에 대한 '접근자'로 실제 객체를 다룰 수 있다.
3. 객체는 <span style=color:red>단 하나만 만들어지며, 만들어진 객체를 공유</span>한다.
 
<문제점>
1. 코드 자체가 많이 필요하다.
2. 테스트하기가 꽤나 어렵다.
3. 자식 클래스를 만들 수 없다.
4. 내부 상태를 변경하기 어렵다.


## 2. 추상 팩토리 패턴
![](https://velog.velcdn.com/images/king33/post/197e1431-adad-419d-82fc-e175464effe7/image.PNG)

추상 팩토리 패턴은 서로 연관이 있는 객체 군이 여러 개 있을 경우 이들을 서로 묶어 '추상화'하고, 어떤 구체적인 상황이 주어지면 팩토리 객체에서 집합으로 묶은 객체 군을 구현화하는 기법이다. 정의만 보면 뭔 갸소리인지 잘 모르겠다. 다시 알기쉽게 표현하자면, 특정 객체에 대한 구현부를 숨겨 역할과 구현을 분리시킨다는 것이다.
-> [관련 있는 객체를 그룹으로 묶어서 생성하는 패턴]

Q. <span style=color:skyblue>언제 사용하는가?</span>
여러 제품군(관련 객체)을 생성해야 하지만, 어떤 제품군을 사용해야 할 지는 코드에서 알 필요가 없을 때
Q. <span style=color:skyblue>어떻게 작동하는가?</span>
"팩토리"라는 공장을 사용해 특정 제품군의 객체들을 한꺼번에 생성한다.
Q. <span style=color:skyblue>쉽게 비유하자면?</span>
가구 공장에서는 한 번에 침대 / 테이블 / 의자같은 제품들을 만들지만, 스타일은 모던 or 클래식 등으로 하나만 선택해 생산한다.

Code
```
// 제품 인터페이스
class Chair {
  sit() {}
}

class Table {
  use() {}
}

// 구체적인 제품들
class ModernChair extends Chair {
  sit() {
    console.log("모던 체어에 앉음");
  }
}

class ClassicChair extends Chair {
  sit() {
    console.log("클래식 체어에 앉음");
  }
}

class ModernTable extends Table {
  use() {
    console.log("모던 테이블 사용");
  }
}

class ClassicTable extends Table {
  use() {
    console.log("클래식 테이블 사용");
  }
}

// 추상 팩토리
class FurnitureFactory {
  createChair() {}
  createTable() {}
}

// 구체적인 팩토리들
class ModernFurnitureFactory extends FurnitureFactory {
  createChair() {
    return new ModernChair();
  }

  createTable() {
    return new ModernTable();
  }
}

class ClassicFurnitureFactory extends FurnitureFactory {
  createChair() {
    return new ClassicChair();
  }

  createTable() {
    return new ClassicTable();
  }
}

// 사용 예시
const factory = new ModernFurnitureFactory();
const chair = factory.createChair();
const table = factory.createTable();

chair.sit(); // 모던 체어에 앉음
table.use(); // 모던 테이블 사용

```
<특징>
1. 제품군을 묶어서 객체를 생성할 수 있다.
2. 구체적인 클래스에 의존하지 않고, 인터페이스를 통해 객체를 생성한다.
3. 서로 관련된 객체들을 일관된 방식으로 생성할 수 있다.
4. 유연성이 높아 다양한 객체군을 쉽게 추가하거나 변경할 수 있다.

<문제점>
1. 새로운 제품군을 추가하려면 인터페이스와 팩토리 클래스를 모두 수정해야 한다.
2. 코드 구조가 복잡해지고, 설계와 구현에 시간이 더 걸릴 수 있다.
3. 모든 제품군이 항상 필요한 것은 아니므로, 불필요한 객체를 생성할 가능성이 있다.
4. 클래스 수가 많아지면서 관리 비용이 증가할 수 있다.

## 3. 팩토리 메소드 패턴
![](https://velog.velcdn.com/images/king33/post/f803777f-d63a-47f0-988a-f2c97747a936/image.PNG)

부모 클래스에서 객체들을 생성할 수 있는 인터페이스를 제공하지만, 자식 클래스에서 생성될 객체들의 유형을 직접 변경할 수 있게 하는 패턴이다.
-> [객체 생성의 책임을 서브클래스로 넘기는 패턴]

Q. <span style=color:skyblue>언제 생성?</span>
객체 생성 코드가 자주 바뀌거나, 어떤 객체를 생성할지 미리 정할 수 없을 때
Q. <span style=color:skyblue>어떻게 작동하는가?</span>
부모 클래스는 객체 생성 메소드를 정의하고, 자식 클래스가 이 메소드를 '오버라이드'하여 실제로 생성할 객체를 직접 결정한다.
Q. <span style=color:skyblue>쉽게 비유하자면?</span>
배달의 민족 앱에서 어떤 음식을 주문할지는 고객(자식클래스)이 결정한다. 앱 자체(부모클래스)에서는 배달 프로세스만 정의함.

Code
```
// 부모 클래스
class Animal {
  makeSound() {}
}

// 구체적인 클래스들
class Dog extends Animal {
  makeSound() {
    console.log("크르르 커ㅓㅓ엉엌엌엉컼ㅋ컹");
  }
}

class Cat extends Animal {
  makeSound() {
    console.log("미야아아아아아ㅏㅏㅏㅏㅏㅏ옹");
  }
}

// 팩토리 클래스
class AnimalFactory {
  createAnimal() {}
}

// 구체적인 팩토리들
class DogFactory extends AnimalFactory {
  createAnimal() {
    return new Dog();
  }
}

class CatFactory extends AnimalFactory {
  createAnimal() {
    return new Cat();
  }
}

// 사용 예시
const dogFactory = new DogFactory();
const catFactory = new CatFactory();

const dog = dogFactory.createAnimal();
const cat = catFactory.createAnimal();

dog.makeSound(); // 짖는중
cat.makeSound();
```
<특징>
1. 객체 생성의 책임을 부모 클래스에서 자식 클래스에 위임한다.
2. 부모 클래스는 객체 생성 방식에 대해 알 필요가 없다.
3. 새로운 객체를 추가하려면 새로운 서브클래스를 정의하면 된다.
4. 단일 책임 원칙과 개방-폐쇄 원칙을 잘 따른다.

<문제점>
1. 클래스 수가 증가하여 코드가 복잡해질 수 있다.
2. 객체 생성 로직이 간단한 경우에도, 불필요하게 팩토리 메소드로 감쌀 가능성이 있다.
3. 설계가 과도하게 추상적일 경우 이해하고 유지보수하는 데 어려움을 겪을 수 있다.
4. 특정 서브클래스에 의존하게 되면, 유연성이 떨어질 수 있다.

---

여기까지 생성패턴 3가지 정도를 알아보았다.
행동패턴과 구조패턴에 대해서는 다음글에 계속 작성한다.

사진출처 - 한빛출판네트워크:[Design pattern] 많이 쓰는 14가지 핵심 GoF 디자인 패턴의 종류
https://www.hanbit.co.kr/channel/category/category_view.html?cms_code=CMS8616098823



![](https://velog.velcdn.com/images/king33/post/7b68803c-dd6f-4b4d-b999-4a957f8bf0b0/image.png)

이전 글에서 디자인 패턴은 크게 3가지로 나뉜다는 것을 알게되었고, 제일먼저 생성 패턴에 대해 먼저 정리하였었다.

이제 나머지 행동 패턴과 구조 패턴에 대해서도 간단히 알아보자.

---

# <span style=color:green>행동 패턴
"객체 간의 책임과 소통을 조직화하고, 효율적으로 협력할 수 있도록 돕는 패턴"
객체들이 상호작용하는 방법과 책임을 분산하는 방식을 정의한다.

## 1. 템플릿 메소드 패턴
![](https://velog.velcdn.com/images/king33/post/f133dc60-e287-4bbb-9be7-db162c8af916/image.PNG)

템플릿 메소드 패턴은 부모 클래스에서 알고리즘의 골격을 정의하지만, 해당 알고리즘의 구조를 따로 변경하지 않고 자식 클래스들이 이 알고리즘의 특정 단계들을 직접 오버라이드(재정의) 할 수 있도록 하는 행동 패턴이다.
(앞서 생성 패턴의 "팩토리 메소드"와 유사하다)
-> [알고리즘의 뼈대를 정의하고, 일부 세부사항은 서브클래스에서 구현하도록 하는 패턴]

Q. <span style=color:skyblue>언제 사용하는가?</span>
공통된 작업 흐름(알고리즘)이 있지만, 일부 단계는 상황에 따라 다르게 동작해야 할 때(ex - 데이터 처리 일반적인 흐름은 같지만, 데이터 형식은 다를 경우:JSON, XML)
Q. <span style=color:skyblue>어떻게 작동하는가?</span>
부모 클래스에서 알고리즘의 전체 구조(템플릿)를 정의하고, 서브클래스가 템플릿의 특정 단계만 오버라이드하여 자신의 방식으로 구현한다.
Q. <span style=color:skyblue>아주 쉽게 비유하자면?</span>
요리 레시피로 비유할 수 있다! 요리 흐름은 재료준비 -> 요리 -> 서빙으로 동일하지만, 요리법은 개개인마다 다 다르다.

Code(JavaScript)
```
class Recipe {
  prepare() {
    this.gatherIngredients();
    this.cook();
    this.serve();
  }

  gatherIngredients() {
    console.log("재료를 준비합니다.");
  }

  cook() {
    throw new Error("서브클래스에서 cook()을 구현해야 합니다.");
  }

  serve() {
    console.log("요리를 서빙합니다.");
  }
}

class GrilledDish extends Recipe {
  cook() {
    console.log("재료를 구워서 요리합니다.");
  }
}

class SteamedDish extends Recipe {
  cook() {
    console.log("재료를 쪄서 요리합니다.");
  }
}

// 사용 예시
const grilledDish = new GrilledDish();
grilledDish.prepare();

const steamedDish = new SteamedDish();
steamedDish.prepare();
```
<특징>
1. 알고리즘의 일관된 흐름을 보장하면서, 일부 단계만 변경할 수 있다.
2. 코드 중복을 줄이고, 재사용성을 높일 수 있다.
3. 부모 클래스에서 핵심 로직을 정의하고, 서브클래스가 구체적인 행동을 구현한다.
4. 개방-폐쇄 원칙을 잘 따른다.

<문제점>
1. 모든 서브클래스가 부모 클래스의 공통 흐름을 따라야 하기 때문에 유연성이 제한될 수 있다.
2. 서브클래스에서 잘못된 오버라이드로 인해 예상치 못한 동작이 발생할 수 있다.
3. 알고리즘이 복잡하면 템플릿 메소드의 코드도 복잡해질 수 있다.


## 2. 상태 패턴
![](https://velog.velcdn.com/images/king33/post/b12f105b-f8cc-42eb-bb81-ee70b803107f/image.PNG)

상태 패턴은 객체의 내부 상태가 변경될 시, 해당 객체가 그 행동을 변경할 수 있도록 하는 행동 패턴이다. 즉, 객체가 행동을 변경할 때 객체가 클래스를 변경한 것처럼 보일 수 있다.
-> [객체의 내부 상태에 따라 다른 행동을 수행하도록 설계하는 패턴]

Q. <span style=color:skyblue>언제 사용하는가?</span>
객체의 동작이 상태에 따라 달라질 때 사용한다. 예시로, 음악 플레이어(재생, 일시 정지, 정지 상태)에 따라 버튼 동작이 달라질 때 이 패턴을 사용할 수 있다.
Q. <span style=color:skyblue>어떻게 작동하는가?</span>
상태를 클래스로 분리하고, 객체의 상태를 변경할 때 행동도 함께 변경되도록 만들어야 한다.
Q. <span style=color:skyblue>아주 쉽게 비유하자면?</span>
TV 리모컨 : TV가 꺼져 있을 때 전원버튼의 역할은 켜는 역할이고, 반대로 TV가 커져 있을 때 전원버튼의 역할은 끄는 역할이다.

Code(JavaScript)
```
class TV {
  constructor() {
    this.state = new OffState();
  }

  setState(state) {
    this.state = state;
  }

  pressButton() {
    this.state.pressButton(this);
  }
}

class OnState {
  pressButton(tv) {
    console.log("TV를 끕니다.");
    tv.setState(new OffState());
  }
}

class OffState {
  pressButton(tv) {
    console.log("TV를 켭니다.");
    tv.setState(new OnState());
  }
}

// 사용 예시
const tv = new TV();
tv.pressButton(); // TV On
tv.pressButton(); // TV Off
```
<특징>
1. 상태에 따른 행동 변경을 쉽게 구현할 수 있다.
2. 조건문 없이 상태 전환 로직을 클래스 간의 연결로 처리한다.
3. 열린 설계로 새로운 상태를 쉽게 추가할 수 있다.
4. 단일 책임 원칙을 잘 따르며, 상태와 행동을 분리한다.

<문제점>
1. 클래스 수가 늘어나고, 코드가 복잡해질 수 있다.
2. 객체 간의 상태 전환이 자주 발생하면 추적이 어려워질 가능성이 있다.
3. 모든 상태에 대해 새로운 클래스를 정의해야 하므로 초기 설계 비용이 높을 수 있다.


## 3. 반복자 패턴
![](https://velog.velcdn.com/images/king33/post/ccf593b8-2e75-4f4e-bc8d-bff358358f21/image.PNG)

얘는 컬렉션의 요소들의 기본 표현(자료구조 - 리스트, 스택, 트리 등)을 노출하지 않고 그들을 하나씩 순회할 수 있도록 하는 행동 패턴이다.
-> [컬렉션(데이터 집합) 요소를 순서대로 접근할 수 있도록 하는 패턴]

Q. <span style=color:skyblue>언제 사용할까?</span>
데이터 구조 내부를 알 필요 없이, 순차적으로 데이터를 순회해야 할 때(ex - 배열, 리스트, 트리 구조의 데이터에 하나씩 접근)
Q. <span style=color:skyblue>어떻게 작동하는가?</span>
컬렉션과 반복 작업을 분리하고, 반복자를 통해 요소에 접근한다.
Q. <span style=color:skyblue>아주 쉽게 비유하자면?</span>
책장에 책이 막 섞여있어도 책은 한 권씩 꺼내볼 수 있다.

Code(JavaScript)
```
class Iterator {
  constructor(collection) {
    this.collection = collection;
    this.index = 0;
  }

  hasNext() {
    return this.index < this.collection.length;
  }

  next() {
    if (this.hasNext()) {
      return this.collection[this.index++];
    }
    return null;
  }
}

// 사용 예시
const items = ["apple", "banana", "cherry"];
const iterator = new Iterator(items);

while (iterator.hasNext()) {
  console.log(iterator.next()); // apple, banana, cherry
}
```
<특징>
1. 데이터 구조를 알 필요 없이, 표준화된 방식으로 요소를 순회할 수 있다.
2. 여러 반복자가 동시에 작동할 수 있다.
3. 데이터 집합과 순회 로직을 분리하여 유연성과 가독성이 높아진다.
4. 단순하면서도 강력한 디자인 패턴으로 자주 사용된다.

<문제점>
1. 모든 데이터 구조에 반복자를 구현하려면 추가 코드 작성이 필요하다.
2.컬렉션이 복잡하거나 동적으로 변경될 경우, 반복 로직이 까다로울 수 있다.
3. 대규모 데이터에서 성능 문제가 발생할 수 있다.

---

# <span style=color:green>구조 패턴
"객체와 클래스 간의 관계를 조직화하여, 효율적이고 유연한 구조를 설계하는 패턴"
레고 블록을 어떻게 조립해나갈 것인가?

## 1. 데코레이터 패턴
![](https://velog.velcdn.com/images/king33/post/5f48716c-e6f4-4b63-b4fe-fd6854a4497d/image.PNG)

데코레이터는 객체들을 새로운 행동들을 포함한 특수 래퍼(wrapper) 객체들 안에 넣어서 위 행동들을 해당 객체들에 연결시키는 구조 패턴이다.

Q. <span style=color:skyblue>언제 사용?</span>
기존 객체를 수정하지 않고, 기능을 유연하게 확장해야 할 때(ex - 텍스트에 서식(볼드, 이탤릭 등)을 추가하거나, 로그 기능을 추가할 때)
Q. <span style=color:skyblue>어떻게 작동할까?</span>
기본 객체를 감싸는 래퍼(wrapper) 객체를 만들어, 새로운 기능을 추가하는 방식이다. 이 때 여러 데코레이터를 체인처럼 연결하여 복합적인 기능을 만들 수 있다.
Q. <span style=color:skyblue>쉽게 비유하면?</span>
우리가 카페가서 아샷추를 먹고 싶을 때 아이스티에 샷추가를 직접 눌러줘야 한다..

Code(JS)
```
class Coffee {
  cost() {
    return 5; // 기본 커피 가격
  }
}

class MilkDecorator {
  constructor(coffee) {
    this.coffee = coffee;
  }

  cost() {
    return this.coffee.cost() + 2; // 우유 추가
  }
}

class SugarDecorator {
  constructor(coffee) {
    this.coffee = coffee;
  }

  cost() {
    return this.coffee.cost() + 1; // 설탕 추가
  }
}

// 사용 예시
let coffee = new Coffee();
coffee = new MilkDecorator(coffee);
coffee = new SugarDecorator(coffee);

console.log(coffee.cost()); // 8 나옴
```
<특징>
1. 객체를 감싸는 방식으로, 기능을 동적으로 추가할 수 있다.
2. 여러 데코레이터를 조합하여 다양한 동작을 만들 수 있다.
3. 기존 객체를 수정하지 않으므로, 개방-폐쇄 원칙을 잘 따른다.

<문제점>
1. 데코레이터가 많아지면 복잡도가 증가한다.
2. 각 데코레이터 클래스가 별도로 정의되어야 하므로, 클래스 수가 늘어난다.

## 2. 프록시 패턴
![](https://velog.velcdn.com/images/king33/post/4406e8d3-1409-494c-bbc6-20b9ef022903/image.PNG)

프록시는 다른 객체에 대한 대체(대리인) 또는 자리표시자를 제공할 수 있는 구조 패턴이다. 프록시는 원래 객체에 대한 접근을 '제어'하므로, 우리의 요청이 원래 객체에 전달되기 전 또는 후에 무언가를 수행할 수 있도록 해야한다.
-> [다른 객체에 대한 접근을 제어하기 위해 대리인을 제공하는 패턴]

Q. <span style=color:skyblue>언제 사용하죠?</span>
객체에 직접 접근하지 않고, 중간에 대리 객체를 통해 접근을 제어해야 할 때(ex - 네트워크 원격 호출, 리소스 로딩 지연 등)
Q. <span style=color:skyblue>어떻게 작동하나요?</span>
실제 객체 대신 프록시 객체를 사용하여, 요청을 가로채거나 제어한다. 이 때, 프록시 객체는 필요할 때만 실제 객체를 초기화하거나 동작을 대행한다.
Q. <span style=color:skyblue>쉽게 비유?!</span>
지하철 개찰구 : 지하철을 타려면 개찰구에서 카드를 찍어야만 개찰구가 열려 통과할 수 있다.

Code(JS)
```
class RealImage {
  constructor(filename) {
    this.filename = filename;
    this.loadFromDisk();
  }

  loadFromDisk() {
    console.log(`${this.filename} 이미지를 디스크에서 로딩 중...`);
  }

  display() {
    console.log(`${this.filename} 이미지를 화면에 표시합니다.`);
  }
}

class ProxyImage {
  constructor(filename) {
    this.filename = filename;
    this.realImage = null;
  }

  display() {
    if (!this.realImage) {
      this.realImage = new RealImage(this.filename); // 실제 객체 초기화
    }
    this.realImage.display();
  }
}

// 사용 예시
const image = new ProxyImage("test.png");
image.display(); // 디스크에서 로드 + 화면에 표시
image.display(); // 이미 로드된 이미지 표시
```
<특징>
1. 객체 접근을 제어하거나, 리소스를 효율적으로 관리할 수 있다.
2. 실제 객체를 필요할 때만 초기화하므로, "지연 로딩"(lazy initialization)이 가능하다.
3. 클라이언트는 프록시 객체를 사용하기 때문에, 실제 객체와 프록시 객체의 인터페이스가 동일해야 한다.

<문제점>
1. 프록시 클래스와 실제 클래스가 동일한 인터페이스를 가져야 하므로, 코드 중복이 발생할 수 있다.
2. 프록시 객체가 많아지면 복잡도가 증가할 수 있다.


## 3. 컴포지트 패턴
![](https://velog.velcdn.com/images/king33/post/fbe05687-2a9b-4e2c-b730-a578e0fcd90d/image.PNG)

컴포지트(복합체) 패턴은 객체들을 '트리' 구조들로 구성한 후, 이러한 구조들을 개별 객체들처럼 작업할 수 있도록 하는 구조 패턴이다.
-> [객체를 트리 구조로 구성하여, 단일 객체와 복합 객체를 동일하게 다루는 패턴]

Q. <span style=color:skyblue>언제 사용?</span>
객체들이 계층적 구조를 이루고, 단일 객체와 그룹 객체를 동일하게 처리해야 할 때(ex - 파일시스템)
Q. <span style=color:skyblue>어떻게 작동?</span>
단일 객체와 복합 객체가 동일한 인터페이스를 구현하여, 재귀적으로 처리
Q. <span style=color:skyblue>쉽게 비유?</span>
그룹 객체 -> 폴더
단일 객체 -> 파일
우리가 프로젝트 코드 등을 다룰 때, 파일과 폴더들은 동일한 레벨로 취급한다. 또한 폴더 내에 또 다른 폴더+파일이 존재할 수 있다.

Code(JavaScript)
```
class Component {
  operation() {
    throw new Error("operation()은 서브클래스에서 구현해야 합니다.");
  }
}

class Leaf extends Component {
  constructor(name) {
    super();
    this.name = name;
  }

  operation() {
    console.log(`Leaf: ${this.name}`);
  }
}

class Composite extends Component {
  constructor(name) {
    super();
    this.name = name;
    this.children = [];
  }

  add(component) {
    this.children.push(component);
  }

  operation() {
    console.log(`Composite: ${this.name}`);
    for (const child of this.children) {
      child.operation();
    }
  }
}

// 사용 예시
const root = new Composite("Root");
const child1 = new Composite("Child1");
const child2 = new Composite("Child2");

const leaf1 = new Leaf("Leaf1");
const leaf2 = new Leaf("Leaf2");

child1.add(leaf1);
child2.add(leaf2);
root.add(child1);
root.add(child2);

root.operation();
```
<특징>
1. 단일 객체와 복합 객체를 동일한 방식으로 처리할 수 있다.
2. 재귀적 구조를 통해, 복잡한 계층 구조를 쉽게 표현할 수 있다.
3. 객체 계층 구조가 자주 변경되는 경우, 유지보수가 용이하다.
<문제점>
1. 객체 계층 구조가 너무 복잡해지면, 구조를 이해하기 어려울 수 있다.
2. 각 객체가 동일한 인터페이스를 구현해야 하므로, 설계와 구현에 신중함이 요구된다.

---

와 이거 다 정리하느라 솔직히 너무 힘들었다.
힘들었던 만큼 절대로 잊어버리지 말자.

사진출처 - 한빛출판네트워크:[Design pattern] 많이 쓰는 14가지 핵심 GoF 디자인 패턴의 종류
https://www.hanbit.co.kr/channel/category/category_view.html?cms_code=CMS8616098823