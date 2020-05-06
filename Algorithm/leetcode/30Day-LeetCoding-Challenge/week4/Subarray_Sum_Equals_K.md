# Subarray Sum Equals K

[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/531/week-4/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/531/week-4/)
~~~
sum(i, j) = sum(0, i) - sum(0, j)를 이용하여

앞의 부분합을 hashmap에 넣은 후 처리
~~~

```java
import java.util.HashMap;

class Solution {
	public int subarraySum(int[] nums, int k) {

		HashMap<Integer, Integer> hm = new HashMap<Integer, Integer>();

		int answer = 0;
		int sums = 0;
		hm.put(sums, 1);
		for (int i = 0; i < nums.length; i++) {
			sums += nums[i];
			answer += hm.getOrDefault(sums - k, 0);
			hm.put(sums, hm.getOrDefault(sums, 0) + 1);
		}

		System.out.println(answer);

		return answer;
	}
}

public class Main {
	public static void main(String[] args) {
		Solution solution = new Solution();

		int[] nums = {0,0,0,0,0,0,0,0,0,0};
		int k = 0;

		solution.subarraySum(nums, k);
	}
}
```