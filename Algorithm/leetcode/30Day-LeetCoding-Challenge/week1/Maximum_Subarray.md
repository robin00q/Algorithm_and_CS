# Maximum Subarray

[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/528/week-1/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/528/week-1/)
~~~
dp를 이용한 최대 연속부분수열을 구하는 문제
~~~

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int a = 0;
        int max = Integer.MIN_VALUE;
        for(int n : nums) {
            a += n;
            max = Math.max(max, a);
            if(a < 0) {
                a = 0;
            }
        }
        return max;
    }
}
```