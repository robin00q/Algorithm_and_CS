# Template Method

템플릿 메서드 패턴이란?

- 어떤 작업을 처리하는 일부분을 서브 클래스로 캡슐화 해서 전체 일을 수행하는 구조는 바꾸지 않으면서 특정 단계에서 수행하는 내역을 바꾸는 패턴????

~~~
1. 추상 메소드 (e.g.) abstract void method(){} => 무조건 재정의 필요

2. 훅 메소드 (e.g.) void method(){} => 무조건 재정의 할 필요 없음

하위 클래스에서 추상 메소드를 구현하고 훅 메소드는 적절하게 오버라이드 하면 된다.
~~~

```java
public abstract class SelectJdbcTemplate<T> {

	public List<T> list(String sql) {
		List<T> list = new ArrayList<T>();
		try (Connection conn =ConnectionManager.getConnection();
		PreparedStatement ps = conn.prepareStatement(sql)) {
			try(ResultSet rs = ps.executeQuery()){
				list = rowMap(rs);
			}
		} catch (Exception e) {
			e.printStackTrace();
		}
		return list;
	}
	public abstract List<T> rowMap(ResultSet rs) throws SQLException;

}
```
~~~
Servlet을 사용할 경우 rowMap(데이터를 데이터베이스에서 가져올 때 처리해야할 컬럼이 다를 경우 이런식으로 추상메소드화를 하여 구현할 수 있다.)
~~~