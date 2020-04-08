# Happy Number

[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/528/week-1/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/528/week-1/)
~~~
Set을 이용한 중복 제거를 통해 해결
~~~

```java
import java.util.HashSet;

class Solution {
    public boolean isHappy(int n) {
        
    	HashSet<Integer> set = new HashSet<Integer>();
    	
    	while(!set.contains(n)) {
    		set.add(n);
    		int next = 0;
    		while(n > 0) {
    			next += (n%10)*(n%10);
    			n /= 10;
    		}
    		n = next;
    		if(n == 1) {
    			return true;
    		}
    	}
    	return false;
    }
}
```