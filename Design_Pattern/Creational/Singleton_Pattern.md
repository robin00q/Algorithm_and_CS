# Singleton Pattern

싱글톤 패턴이란?

- 정의 : 전역 변수를 사용하지 않고 객체를 하나만 생성 하도록 하며, 생성된 객체를 어디에서든지 참조할 수 있도록 하는 패턴

- 하나의 인스턴스만을 생성한다. (여러 클라이언트가 동시에 요청한다면 Race Condition 이 발생 가능)
	- synchronized 를 사용해서 crtical section 들어가지 못하도록 조정

```java
public class Printer {
   // 외부에 제공할 자기 자신의 인스턴스
   private static Printer printer = null;
   private int counter = 0;
   private Printer() { }
   // 인스턴스를 만드는 메서드 동기화 (임계 구역)
   public synchronized static Printer getPrinter(){
     if (printer == null) {
       printer = new Printer(); // Printer 인스턴스 생성
     }
     return printer;
   }
   public void print(String str) {
     // 오직 하나의 스레드만 접근을 허용함 (임계 구역)
     // 성능을 위해 필요한 부분만을 임계 구역으로 설정한다.
     synchronized(this) {
       counter++;
       System.out.println(str + counter);
     }
   }
}
```
참고 : [https://gmlwjd9405.github.io/](https://gmlwjd9405.github.io/)