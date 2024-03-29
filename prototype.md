# 🎯 prototype

JS는 명령형, 함수형, 프로토타입 기반 객체지향 프로그래밍을 지원하는 멀티 패러다임 프로그래밍 언어다.

> 타 언어(C++, java)같은 클래스 기반 객체지향 언어인 특징을 모두 갖고있지 않아서 객체지향 언어가 아니라는 오해를 받지만 더 효율적이고, 강력한 객체지향 프로그래밍 능력을 가지고있는 **프로토타입 기반의 객체지향 프로그래밍 언어다.**

#### 👀 Js의 Class

Es6 이후 도입되었지만 기존의 프로토타입을 폐지하고 새로운 객체지향 모델이 나온것이 아니다. <br>Class도 함수이고, 프로토타입 기반의 인스턴스를 생성하지만 정확히 동일하게 작동하진 않으며 생성자함수보다 엄격하고 함수에선 제공하지않는 추가된 기능도 제공한다.
<br>따라서 **새로운 객체 생성 메커니즘**으로 보는것이 합당하다.

---

## 객체지향

전통적인 명령형 프로그래밍의 절차지향적 관점에서 벗어나 여러개의 객체의 집합으로 프로그램을 표현하는 프로그래밍 패러다임이다.

- 특징
  - 인간이 이해하기 쉬운 패러다임 (실세계의 실체를 인식하는 철학적 사고)
  - 실체의 특징이나 성질을 나타내는 속성을 가지고 있다. (eg. 사람 = {이름, 성별, 나이 })
  - 추상화

> 다양한 속성중에서 프로그래밍에 필요한 속성만 간추려 표현하는 것을 **추상화** 라고한다.

```JavaScript
// 추상화, 상태
const person = {
    name: 'yu-ratel',
    age: 27,
};

// 동작
agePuls() {
    return this.age + 1;
}

console.log(person.agePuls()) //28

// 속성을 통해 여러개의 값을 하나의 단위로 구성한 복합적인 자료구조 === 객체
// 상태(프로퍼티)와 동작(메서드)을 하나의 논리적인 단위로 묶은 복합적인 자료구조 === 객체지향 프로그래밍
```

> 각 객체는 독립적인 부품이지만 서로 상호작용(관계성)을 가질 수 있다.<br>
> eg. 다른 객체와 메시지를 주고받거나 데이터처리, 다른객체 상속 등

---

## 상속과 프로토타입

상속은 객체지향 프로그래밍의 핵심 개념으로, 다른객체가 상태(프로퍼티)와 동작(메서드)을 상속받아 사용할 수 있는 것을 말한다.

생성자함수는 동일한 상태와 동작구조를 갖는 객체를 여러개 생성할 때 유리하지만 프로퍼티값이 달라야 한다면 모든 인스턴스가 모든 상태와 동작구조를 중복 소유하는건 메모리를 낭비하며, 퍼포먼스에도 악영향을 주기 때문에 불필요한 중복을 제거 해야한다.

```JavaScript
// 상속 x
function Circle(radius) {
    this.radius = radius;
    this.sum = function () {
        return this.radius + 5;
    }
}

const circle1 = new Circle(5); // 이 안에는 위의 생성자함수의 상태 동작구조가 다 들어있다.
const circle2 = new Circle(10)

console.log(circle1.sum === circle2.sum) // false;

console.log(circle1.sum()) // 10;
console.log(circle2.sum()) // 15;

// 상속 o
function Circle(radius) {
    this.radius = radius;
}

Circle.prototype.sum = function () {
    return this.radius + 5;
}

console.log(circle1.sum === circle2.sum) // true;

const circle1 = new Circle(5);
const circle2 = new Circle(10)

console.log(circle1.sum()) // 10;
console.log(circle2.sum()) // 15;
```

위와 같이 상속은 코드의 재활용이란 관점에서 매우 유용하며 Js는 별도의 구현없이 상위객체인 프로토타입의 자산을 공유하여 상속을 할 수 있다.<br>

> **JS는 프로토타입을 기반으로 상속을 구현**하여 적극적인 코드의 재사용으로 불필요한 중복을 제거함으로서 개발비용을 현저히 줄이는등 다양한 잠재력이 있다.

---

## 프로토타입 객체

프로토타입 객체란 객체 간 상속을 구현하기 위해 사용된다.

모든 객체는 [[prototype]] 이라는 내부 슬롯을 가지며 객체가 생성될 때 마다 생성 방식에 따라(함수, 객체, 배열 등) 프로토타입이 결정되고 [[prototype]]에 저장된다.

> eg. Object.prototype, Array.prototype <br>
> 모든 객체는 하나의 프로토 타입을 가지며, 생성자 함수와 연결되어 있다.

내부슬롯에 저장되어있어 직접 접근이 불가능한 것을 **proto ** 접근자 프로퍼티를 통해 간접적으로 접근할 수 있으며 <br>프로토타입 자신의 constructor 프로퍼티를 통해 생성자 함수에 접근할 수 있고, 생성자함수는 자신의 prototype 프로퍼티를 통해 프로토타입에 접근할 수 있다.

- **proto ** 접근자 프로퍼티

  - 자신의 프로토타입 내부슬롯에 간접적으로 접근할 수 있다.
  - 자체적인 값을 갖지않고, 프로퍼티 어트리뷰트(get, set)로 구성된 프로퍼티다.
  - 상속을 객체가 직접 소유하는 프로퍼티가 아닌 상위의 프로퍼티다. (eg. 객체 => object.prototype)
  - 프로토타입 체인은 서로가 자신의 프로토타입이 되는 양방향 참조(순환참조, 종점이 없는 무한루프)를 막기위해 단방향 링크드 리스트여야 해서 proto 접근자 프로퍼티를 이용해 접근하고 교체한다.
  - 코드내에선 직접 사용을 권장하지 않는다(모든 객체가 접근자 프로퍼티를 사용할 순 없기에)
    > 코드 내에선 es5, es6 이후 등장한 동일한 역할을 해주는 getPrototypeOf, setPrototypeOf 등을 사용하는것을 권장한다.

- 함수 객체의 prototpye 프로퍼티

  - 함수 객체만이 소유하는 porototype 프로퍼티는 그 함수가 생성한 인스턴스의 프로토타입을 가리킨다.

    > 즉 생성자함수가 아닌 일반 객체는 prototype을 소유하지 않는다. <br>
    > => non-constructor(화살표 함수 등)은 prototype 프로퍼티가 존재하지않고 프로토타입도 생성하지 않는다.

  - 함수 객체의 prototpye 프로퍼티는 생성자 함수가 생성하는 인스턴스에 프로토타입을 할당하기 위해 사용하고, 접근자 프로퍼티는 상위에서 객체가 접근 또는 교체하기 위해 사용한다.
    > 결국 둘다 똑같은 프로토타입을 가리키지만 이들을 사용하는 주체가 다르다.

- 프로토타입의 constructor 프로퍼티와 생성자함수
  - 모든 프로토타입은 constructor 프로퍼티를 갖는다
    > constructor -> 함수 객체가 생성될 때 이뤄지며, 자신을 참조하고 있는 생성자 함수를 가리킨다. 따라서 체이닝(인스턴스에 없어도 부모에서 끌어와서 사용가능)이 가능하다.

---

## 리터럴 표기법에 의해 생성된 객체의 생성자 함수와 프로토타입

명시적으로 new 연산자와 생성자함수를 호출하여 인스턴스를 생성하지 않는 방식

```JavaScript
const obj = {};
const add = functon(a, b) {return a + b};
```

객체이기에 프로토타입이 물론 존재하지만, 명시적이기 않기 때문에 constructor 프로퍼티가 반드시 생성한 함수를 가리킨다고 지정할 수 없다.

> 추상연산(자체적으로 객체 상위의 prototype을 가리킴)을 호출하여 빈객체를 생성하고 프로퍼티를 추가하지만, 세부내용은 달라서 리터럴에 의해 생성된 객체는 생성자 함수가 생성한 객체가 아니다. (가상적인 생성자 함수를 갖는다.)

**따라서 생성자함수를 호출하지 않아도 결국 프로토타입은 단독으로 존재할 수 없고, 쌍으로 존재한다.**

> 함수를 예시 => 하지만 미묘한 차이가 있을 뿐(스코프, 클로저 등) 결국 함수로서 동일한 특성을 갖는다. 따라서 생성자함수를 리터럴 표기법으로 생성한 객체 또한 생성한 생성자 함수로 생각해도 크게 무리는 없다. <br>
> eg. Object.prototype, Function.prototype ...
