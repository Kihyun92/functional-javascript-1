# 함수형 자바스크립트

## 함수형 프로그래밍이란 무엇일까?

* 순수함수로 프로그래밍을 하는 것
* 함수로 기능을 추상화해서 프로그래밍 하는 것
* 이미 입증된 함수로 새로운 함수로 만들어서 프로그래밍 하는 것
* 상태변이를 최소화하면서 프로그래밍하는 것

> FP와 OOP가 전혀 다른 패러다임이라는 사고방식은 객체를 정의하는 전통적인 방향 때문에 생긴 오해인듯 싶다며. 객체는 상태와 동작을 묶은 캡슐이라는 기존의 시각에선.. 함수도 객체라는 관점이 성립하기 어려워지니까. 그러나 실제로 함수는 객체와 전혀 다른 무엇이 아니라, “상태가 없는 객체”라는 관점으로 보는 것이 적절하다며. 따라서 객체 = 상태 + 동작이라는 시각이 수정된다면.. FP는 단지 동작만 갖고 있는 객체의 조합을 통해 코딩하는 방식으로 정의되어 OOP속으로 들어오게 된다고 말할 수 있게 된다며. 상태없이 동작만 있는 ADT만으로 객체 구성원들이 모두 표현이 된다면 ‘상태변이’라는 변수를 추적해야하는 기존 OOP가 갖고 있는 고질적인 문제에서 조금 더 예측하기 쉬운 코드로 표현되는 OOP로 개선될 수 있는데 이점을 그냥 FP라고 부를 뿐이람서. FP와 OOP는 패러다임이 다른 것이 아니라 모델이 다를 뿐이라며.

## 부수 효과가 없다는 것은 무엇인가?

* 효과가 아닌 것.
* 함수의 결과가 오직 파라미터에 의해서만 결정되는 것
* 외부 변수에 의존하지 않는다.
* 외부에 의해 영향을 받지 않는다.
* 외부에 영향을 주지 않는다.

## 효과란?

* 함수 반환값에 의해서만 변경이 일어나는 것

### 예시

```js
const sum = (a, b) => a + b;
```

```js
let other;

const sum = (a, b) => {
  other = a + b;
};
```

## 함수형 프로그래밍을 왜 해야할까?

* 복잡한 코드를 간결하게 분리할 수 있다.
* 선언적으로 할 수 있다.
* 테스트가 용이하다.
* 더 안전하게 프로그래밍할 수 있다.
* 순수한 순수하지 않은 부분을 명확하게 나눌 수 있다.

## 선언적인 프로그래밍이란?

* 결과만 기술할 뿐 어떻게는 기술하지 않는 프로그래밍 방법
* 의도에 집중한 프로그래밍 방법

### 함수란 무엇인가?

* 방정식 1 + 2 = 3이다. 같은 파라미터는 같은 결과가 나온다.
* 수학적 정의와 프로그래밍에서의 정의는 없다.
* 뭐 넣으면 뭐 나온다.

## 함수형 프로그래밍의 특징이란 무엇인가?

* 부수효과를 최소화한다.
* 선언적으로 한다.
* 결합도가 약해서 유연하다.
* 함수자체만으로 재사용할 수 있다.
* 기능을 함수로 분리한다.
* 불변 데이터를 사용한다.

```js
class Person {
  first = '';
  middleName = '';
  last = '';

  // 객체지향
  getFullName() {
    return this.first + this.last;
  }
}

// 함수형
const getName = (person: Person) => [person.firstName, person.lastName].join();
getName(person);
```

### Value Object 패턴이란 무엇일까?

* 오직 값에 좌우되는 객체
* 객체를 선언한 이후엔 그 상태가 절대 변하지 않는 것

### 참조 투명성이란? 무엇일까?

* 함수를 값으로 대체할 수 있는 것
* 순수성이랑 같은 의미다.

```js
const sum = (a, b) => {
  return a + b;
};

const value = sum(3, 4);
console.log('value: ', value); // value: 7
```

### 커링이란 무엇일까?

* 인자가 여러개를 받는 함수를 인자 하나씩만 받도록 만드는 것

### 커링을 왜 할까?

* 함수 합성을 쉽게하기 위해서 파라미터가 하나인 함수를 만들기 위해서
* 매개변수의 처리에 대한 책임을 나누기 위해서
* 중간과정에 개입할 수 있는 여지를 만들 수 있다.

```js
const arr = ['1', '2', '3'];

const curriedParseInt = (radix) => (value) => parseInt(value, radix);

const toDecimal = someFunction(curriedParseInt(10));
const toHex = curriedParseInt(16);

arr.map(toDecimal);
```

### 커링을 적용한 함수는?

* 커리된 함수라고 부른다.

### 단항함수

* 인자를 하나만 받는 함수

## 함수형/객체지향은 어떤 차이가 있는가?

차이가 없다.

객체지향은 데이터와 기능이 깊게 결합되어 있다.
상태를 가지고 프로그래밍한다.
객체들을 조합해서 프로그래밍하는 것. 기능이 객체단위로 있다.

함수는 데이터와 기능을 느슨하게 연결한다.
상태와 기능을 철저히 분리한 다음 이들을 다시 조합한 새로운 함수로 연산을 추가할 수 있다.
문제들을 작은 함수로 잘게 나눈다.
상태 없이 프로그래밍한다.
기능단위로 작게 나눠서 함수로 분리하고, 그 함수를 조합하여 프로그래밍하는 것이다. 이 함수들은 이미 입증이 되어있어서 쉽게 안전한 프로그램을 만들 수 있다.

## High order function이란 무엇일까?

## first class(일급 시민)이라는 것은 무엇일까?

## 클로저란 무엇일까?

## See also

* 함수형 프로그래밍이란 무엇인가? - https://medium.com/@jooyunghan/%ED%95%A8%EC%88%98%ED%98%95-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80-fab4e960d263
* 함수형 자바스크립트 - http://www.kyobobook.co.kr/product/detailViewKor.laf?barcode=9791162240427