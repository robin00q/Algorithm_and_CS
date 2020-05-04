# First Bad Version

[https://leetcode.com/explore/challenge/card/may-leetcoding-challenge/534/week-1-may-1st-may-7th/](https://leetcode.com/explore/challenge/card/may-leetcoding-challenge/534/week-1-may-1st-may-7th/)
~~~
이분탐색을 이용한 최솟값 찾기
~~~


```java
/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */

public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int ans = Integer.MAX_VALUE;
        
        int l = 1;
        int r = n;
        while(l <= r){
            int mid = l + (r - l) / 2;
            
            if(isBadVersion(mid)){
                ans = Math.min(ans,mid);
                r = mid - 1;
            } else {
                l = mid + 1;
            }
        }
        
        return ans;
    }
}
```