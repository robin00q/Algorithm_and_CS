# Jump Game

[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/531/week-4/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/531/week-4/)
~~~
linear로 최대한 갈 수 있는 곳을 확인하여 끝까지 갈 수 있다면 정답을 출력
~~~

```java
class Solution {
	public boolean canJump(int[] nums) {

		if (nums.length == 1) {
			return true;
		}
		if (nums[0] == 0) {
			return false;
		}

		int reachable = 0;
		for (int i = 0; i < nums.length - 1; i++) {
			reachable = Math.max(nums[i], reachable - 1);
			if (reachable + i >= nums.length - 1) {
				return true;
			}
			if (reachable == 0) {
				return false;
			}
		}

		return false;
	}
}

public class Main {
	public static void main(String[] args) {
		Solution sol = new Solution();

		int[] nums = { 2, 3, 1, 1, 4 };
		sol.canJump(nums);

	}
}
```