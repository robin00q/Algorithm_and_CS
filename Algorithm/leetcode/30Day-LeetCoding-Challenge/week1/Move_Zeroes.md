# Move Zeroes

[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/528/week-1/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/528/week-1/)
~~~
추가로 다른 배열을 사용하지 않고 모든 0을 제외한 숫자를 앞으로 당기는 문제
~~~

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int pos = 0;
        
        for(int n : nums) {
            if(n != 0) {
                nums[pos++] = n;    
            }
        }
        Arrays.fill(nums, pos, nums.length, 0);
    }
}
```