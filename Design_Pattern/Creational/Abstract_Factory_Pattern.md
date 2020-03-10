# Abstract Factory

추상 팩토리 패턴이란?

- 정의 : 추상적인 abstract class factory 내부에 객체를 골라서 생성할 수 있도록 (abstract class) 하는 패턴

- 관련 객체들 끼리 연관성이 있는 경우 종류별로 별도의 Factory를 쓰는 것 보다 관련 객체들을 일관성 있게 생성하는 Factory 클래스를 사용하는 것이 편리하다??????
~~~
- 즉 이말은 Motor Factory, Door Factory, Wire Factory, .... 이렇게 많은 경우 

- 이 부품들을 삼성, LG, 기아, 현대 등 에서 생산할 경우 

- Hyundai Factory 안에 Motor, Door, Wire ... 을 생성하도록 클래스를 주는 것이 낫다는 것이다.

- 그리고 LG, 기아, 현대 등은 추상 팩토리에서 abstract로 만들어 원하는 것을 생성하도록 하는 것이다.

아래의 그림처럼...
~~~
![Abstract Factory](https://gmlwjd9405.github.io/images/design-pattern-abstract-factory/abstract-factory-solution1.png)

참고 : [https://gmlwjd9405.github.io/](https://gmlwjd9405.github.io/)