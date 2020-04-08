# Group Anagrams

[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/528/week-1/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/528/week-1/)
~~~
aet, eat, tea는 모두 sort하면 aet로 문자순서대로 변하는 것을 이용
~~~

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashMap;
import java.util.List;

class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
    	HashMap<String, List<String>> hm = new HashMap<String, List<String>>();
    	
    	List<List<String>> lls = new ArrayList<List<String>>();
    	
        for(String x : strs) {
        	char[] cArr = x.toCharArray();
        	Arrays.sort(cArr);
        	List<String> ls;
        	if(hm.get(String.valueOf(cArr)) == null) {
        		ls = new ArrayList<String>();
        	} else {
        		ls = hm.get(String.valueOf(cArr));
        	}
        	ls.add(x);
        	hm.put(String.valueOf(cArr), ls);
        }
        
        for(String key : hm.keySet()) {
        	lls.add(hm.get(key));
        }
        
        return lls;
    }
}
```