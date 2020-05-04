# Ransom Note

[https://leetcode.com/explore/challenge/card/may-leetcoding-challenge/534/week-1-may-1st-may-7th/](https://leetcode.com/explore/challenge/card/may-leetcoding-challenge/534/week-1-may-1st-may-7th/)
~~~
HashMap을 이용하여 magazine이 ransonNote에 포함된 character 개수 이상 갖고있는지 확인
~~~

```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        Map<Character, Integer> m1 = new HashMap<Character, Integer>();
        Map<Character, Integer> m2 = new HashMap<Character, Integer>();
        
        int ans = 0;
        for(char ch : magazine.toCharArray()){
            m1.put(ch, m1.getOrDefault(ch, 0) + 1);
        }
        for(char ch : ransomNote.toCharArray()){
            m2.put(ch, m2.getOrDefault(ch, 0) + 1);
        }
        
        Iterator<Character> it = m2.keySet().iterator();
        while(it.hasNext()){
            Character key = it.next();
            if(m2.get(key) > m1.getOrDefault(key, 0)){
                return false;
            }
        }

        return true;
    }
}
```