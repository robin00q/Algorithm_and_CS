# Last Stone Weight

[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/529/week-2/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/529/week-2/)
~~~
PriorityQueue의 위의 2개를 지속적으로 뺴주는 문제
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

import java.util.Comparator;
import java.util.PriorityQueue;

class Solution {
    public int lastStoneWeight(int[] stones) {
    	int answer = 0;
        PriorityQueue<Integer> pq = new PriorityQueue<Integer>(new Comparator<Integer>() {
			@Override
			public int compare(Integer o1, Integer o2) {
				return o2 - o1;
			}
		});
        
        for(int s : stones) {
        	pq.add(s);
        }
        
        while(!pq.isEmpty()) {
        	if(pq.size() == 1) {
        		answer = pq.poll();
        		break;
        	}
        	int a = pq.poll();
        	int b = pq.poll();
        	pq.add(a - b);
        }
        System.out.println(answer);
        return answer;
    }
}
```