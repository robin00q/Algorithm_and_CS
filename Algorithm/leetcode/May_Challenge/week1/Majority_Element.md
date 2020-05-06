# Majority Element

[https://leetcode.com/explore/challenge/card/may-leetcoding-challenge/534/week-1-may-1st-may-7th/](https://leetcode.com/explore/challenge/card/may-leetcoding-challenge/534/week-1-may-1st-may-7th/)
~~~
hashmap을 사용한 가장 많이 등장한 element 추출
~~~


```java
import java.util.HashMap;
import java.util.Iterator;

class Solution {
	public int majorityElement(int[] nums) {
		HashMap<Integer, Integer> hm = new HashMap<Integer, Integer>();

		for (int n : nums) {
			hm.put(n, hm.getOrDefault(n, 0) + 1);
		}

		Iterator<Integer> it = hm.keySet().iterator();

		int answer = -1;
		int max = 0;
		while (it.hasNext()) {
			int key = it.next();
			if (max < hm.get(key)) {
				answer = key;
				max = hm.get(key);
			}
		}
		return answer;
	}
}
```