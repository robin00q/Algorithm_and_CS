# Backspace String Compare

[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/529/week-2/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/529/week-2/)
~~~
간단한 문자열 추가 문제
~~~

```java
class Solution {
    public boolean backspaceCompare(String S, String T) {
        
    	if(makeString(S).equals(makeString(T))) {
    		return true;
    	}
    	return false;
    }

	private String makeString(String str) {
		String ret = "";
    	
    	int sLen = str.length();
    	for(int i = 0 ; i < sLen ; i++) {
    		if(str.charAt(i) == '#') {
    			if(!ret.isEmpty()) {
    				ret = ret.substring(0, ret.length()-1);
    			}
    		} else {
    			ret += str.charAt(i);
    		}
    	}
    	System.out.println(ret);
    	return ret;
	}
}
```