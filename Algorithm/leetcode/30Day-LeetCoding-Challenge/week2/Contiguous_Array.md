# Contiguous Array

[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/529/week-2/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/529/week-2/)
~~~
0과 1로만 이루어진 배열이 있을 때 가장 긴 0과 1의 개수가 같은 이어지는 array의 길이를 반환하라

0과 1에 대해서 0은 +1, 1은 -1을 하여 길이 : idx의 hashmap을 만들어 0번과 끝번의 차이의 최대값을 반환
~~~

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;

class Solution {
	public int findMaxLength(int[] nums) {
		int answer = 0;
		HashMap<Integer, List> hm = new HashMap<Integer, List>();

		List<Integer> l = new ArrayList<Integer>();
		l.add(0);
		hm.put(0, l);
		
		int count = 0;
		for (int i = 0; i < nums.length; i++) {
			if (nums[i] == 0) {
				count++;
			} else {
				count--;
			}
			List<Integer> newList = hm.get(count);
			if (newList == null) {
				newList = new ArrayList<Integer>();
			}
			newList.add(i+1);
			hm.put(count, newList);
		}

		for (Integer key : hm.keySet()) {
			List<Integer> getList = hm.get(key);
			int maxLen = getList.get(getList.size() - 1).intValue() - getList.get(0).intValue();
			answer = Math.max(answer, maxLen);
		}
		return answer;
	}
}
```