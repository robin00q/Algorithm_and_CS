# Product of Array Except Self

[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/530/week-3/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/530/week-3/)
~~~
자신을 제외한 나머지 배열의 곱을 구하는 문제

부분곱을 이용하여 해당 점에서 pre, suffix의 곱을 구해 연산한다.
~~~

```java
class Solution {
	public int[] productExceptSelf(int[] nums) {

		int answer[] = new int[nums.length];
		int premult[] = new int[nums.length + 1];
		int sufmult[] = new int[nums.length + 1];

		premult[0] = 1;
		sufmult[nums.length] = 1;
		for (int i = 0; i < nums.length; i++) {
			premult[i + 1] = premult[i] * nums[i];
		}

		for (int i = nums.length - 1; i >= 0; i--) {
			sufmult[i] = sufmult[i + 1] * nums[i];
		}

		for (int i = 0; i < answer.length; i++) {
			if(i-1 < 0) {
				answer[i] = sufmult[i+1];
			} else if(i+1 > answer.length) {
				answer[i] = premult[i-1];
			} else {
				answer[i] = premult[i] * sufmult[i+1];
			}
		}
		
		return answer;
	}
}
```