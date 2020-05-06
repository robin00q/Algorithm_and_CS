# First Unique Character in a String

[https://leetcode.com/explore/challenge/card/may-leetcoding-challenge/534/week-1-may-1st-may-7th/](https://leetcode.com/explore/challenge/card/may-leetcoding-challenge/534/week-1-may-1st-may-7th/)
~~~
easy problem
~~~


```java
import java.util.Arrays;

class Solution {

	public int firstUniqChar(String s) {
		int[] arr = new int[26];
		boolean[] valid = new boolean[26];

		Arrays.fill(valid, true);
		Arrays.fill(arr, -1);

		for (int i = 0; i < s.length(); i++) {
			char ch = s.charAt(i);
			if (arr[ch-'a'] == -1) {
				arr[ch-'a'] = i;
			} else {
				valid[ch-'a'] = false;
			}
		}
		int answer = Integer.MAX_VALUE;
		for (int i = 0; i < 26; i++) {
			if (valid[i] == true && arr[i] != -1) {
				answer = Math.min(answer, arr[i]);
			}
		}

		if (answer == Integer.MAX_VALUE) {
			return -1;
		}

		return answer;
	}
}

```