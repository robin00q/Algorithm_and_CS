# Perform String Shifts

[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/529/week-2/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/529/week-2/)
~~~
String shift

왼쪽, 오른쪽을 구분하지 않고

왼쪽 = String길이 - 왼쪽 shift길이로 하여 모두 오른쪽 shift로 만든다.

다 더한 뒤 % String.length를 하여 shift
~~~

```java
class Solution {
	public String stringShift(String s, int[][] shift) {

		int count = 0;
		for (int[] arr : shift) {
			if (arr[0] == 0) {
				count += s.length() - arr[1];
			} else {
				count += arr[1];
			}
		}

		count %= s.length();
		
		s = s.substring(s.length()-count, s.length()) + s.substring(0, s.length()-count);
		System.out.println(s);

		return s;
	}
}
```