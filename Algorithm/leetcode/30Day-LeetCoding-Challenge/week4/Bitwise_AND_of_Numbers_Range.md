# Bitwise AND of Numbers Range

[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/531/week-4/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/531/week-4/)
~~~

n과 m을 포함한 사이의 수를 모두 and한 결과를 추출하라

prefix가 다르기 전 까지의 n과 m을 출력하면 된다.
~~~

```java
class Solution {
	public int rangeBitwiseAnd(int m, int n) {
		int ans = 0;
		int start = 1 << 30;

		while (start > 0) {
			if ((start & m) != (start & n)) {
				break;
			} else {
				ans += (start & m);
			}
			start = start >> 1;
		}
		
		System.out.println(ans);
		return ans;
	}
}
```