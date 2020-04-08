# Single Number

[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/528/week-1/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/528/week-1/)
~~~
int 배열 안에 숫자가 들어있다.

어떤 한 숫자를 제외하고 모든 다른 숫자는 2회 등장할 때 한번만 등장하는 숫자를 출력하라.
~~~

```java
class Solution {
    public int singleNumber(int[] nums) {
        
    	int ans = 0;
    	for (int i : nums) {
			ans ^= i;
		}
    	
    	return ans;
    }
}
```