# Decorator

데코레이터 패턴이란?

정의 : 객체의 결합을 통해 기능을 동적으로 유연하게 확장 하도록 하는 패턴

예시) 도로에서 무언가를 그리고 싶을 때

Decorator 패턴이 적용되지 않았을 때
![NOT Decorated](https://gmlwjd9405.github.io/images/design-pattern-decorator/decorator-problem3.png)

Decorator 패턴이 적용됐을 때
![Decorated](https://gmlwjd9405.github.io/images/design-pattern-decorator/decorator-solution.png)

~~~
이와 같이 공통적인 기능이 되는 경우 

아래와 같은 연쇄적인 코드 작성을 통해 추가하는 것
~~~
```java
public class CrossingDecorator extends DisplayDecorator {
  // 기존 표시 클래스의 설정
  public CrossingDecorator(Display decoratedDisplay) { super(decoratedDisplay); }
  @Override
  public void draw() {
      super.draw(); // 설정된 기존 표시 기능을 수행
      drawCrossing(); // 추가적으로 교차로를 표시
     }
  // 교차로 표시 기능만 직접 제공
  private void drawCrossing() { System.out.println("\t교차로 표시"); }
}
```
~~~
메인에서는 아래와 같이 호출하면 draw한번에 모든 클래스의 draw가 호출된다.
~~~
```java
public class Client {
  public static void main(String[] args) {
    // 기본 도로 표시 + 차선 표시 + 교통량 표시 + 교차로 표시
    Display roadWithCrossingLaneAndTraffic =
      new LaneDecorator(
      new TrafficDecorator(
      new CrossingDecorator(
      new RoadDisplay())));
    roadWithCrossingLaneAndTraffic.draw();
  }
}
```
참고 : [https://gmlwjd9405.github.io/](https://gmlwjd9405.github.io/)