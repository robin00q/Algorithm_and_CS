# Jewels and Stones

[https://leetcode.com/explore/challenge/card/may-leetcoding-challenge/534/week-1-may-1st-may-7th/](https://leetcode.com/explore/challenge/card/may-leetcoding-challenge/534/week-1-may-1st-may-7th/)
~~~
HashMap을 이용하여 해당문자가 몇개인지 찾기
~~~


```java
class Solution {
    public int numJewelsInStones(String J, String S) {
        Map<Character, Integer> m = new HashMap<Character, Integer>();
        
        int ans = 0;
        for(char ch : S.toCharArray()){
            m.put(ch, m.getOrDefault(ch, 0) + 1);
        }
        for(char ch : J.toCharArray()){
            ans += m.getOrDefault(ch, 0);
        }
        return ans;
    }
}
```