# Number Complement

[https://leetcode.com/explore/challenge/card/may-leetcoding-challenge/534/week-1-may-1st-may-7th/](https://leetcode.com/explore/challenge/card/may-leetcoding-challenge/534/week-1-may-1st-may-7th/)
~~~
num의 첫 비트를 찾기까지의 합을 prefix로 구한후

(~num) ^ prefix를 하면 앞의 비트를 0으로 만들어 정답을 알아낸다.

>>>를 이용하여 -가 유지되지 않는 bit연산을 사용
~~~


```java
class Solution {
    public int findComplement(int num) {
        
    	int prefix = 0;
    	int bit = 1<<31;
    	while(bit != 0) {
    		if((bit & num) > 0) {
    			break;
    		}
    		prefix += bit;
    		bit = bit >>> 1;
    	}
    	
    	return (~num) ^ prefix;
    }
}
```