# Counting Elements

[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/528/week-1/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/528/week-1/)
~~~
easy..
~~~

```java
import java.util.Arrays;

class Solution {
    public int countElements(int[] arr) {
        
    	Arrays.sort(arr);
    	int answer = 0;
    	int count = 1;
    	
    	for(int i = 0 ; i < arr.length-1 ; i++) {
    		if(arr[i] == arr[i+1]) {
    			count++;
    		} else {
                if(arr[i] + 1 == arr[i+1]) {
    			    answer += count;
                }
    			count = 1;
            }    
    	}
    	
    	return answer;
    }
}
```