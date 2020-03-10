Observer

옵저버 패턴이란?

- 정의 : 한 객체의 상태 변화에 따라 다른 객체의 상태도 연동되도록 일대다 객체 의존 관계를 구성 하는 패턴

- 데이터의 변경이 발생했을 경우 상대 클래스나 객체에 의존하지 않으면서 데이터 변경을 통보하고자 할 때 유용하다.

![Observer](https://gmlwjd9405.github.io/images/design-pattern-observer/observer-solution.png)

~~~
Subject에서는 Observer에게 알리는 nodifyObserver, observer를 추가 제거하는 메소드를 구성

main에서 attach를 통해 observer를 등록하고 addScore를 부르면 

Observer의 인터페이스를 구현한 DataSheetView와 MinMaxView가 update를 수행하도록 함.
~~~

참고 : [https://gmlwjd9405.github.io/](https://gmlwjd9405.github.io/)