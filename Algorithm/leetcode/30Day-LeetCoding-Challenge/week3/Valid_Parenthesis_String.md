# Valid Parenthesis String

[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/530/week-3/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/530/week-3/)
~~~
((*))((()(*** 인 경우 *이 공백이나 (, )로 대체 될 떄 Valid한지 체크한다.

어떻게?

*을 제외하고 생각하면

그림을 그렸을 때 위, 아래로 그리면 0이하로 가면 안됨
따라서 *을 그냥 +1로 생각해서 맞출 수 있음

하지만 반대도 체크해야함

자세한 설명은 아래 링크
~~~

[https://www.youtube.com/watch?v=piT58dNLPhg](https://www.youtube.com/watch?v=piT58dNLPhg)

```java
class Solution {
	public boolean checkValidString(String s) {

		int balance = 0;
		for(int i = 0 ; i < s.length() ; i++) {
			char cur = s.charAt(i);
			if(cur == '(' || cur == '*') {
				balance++;
			} else {
				balance--;
				if(balance == -1) {
					return false;
				}
			}
		}
		
		s = new StringBuilder(s).reverse().toString();
		balance = 0;
		for(int i = 0 ; i < s.length() ; i++) {
			char cur = s.charAt(i);
			if(cur == ')' || cur == '*') {
				balance++;
			} else {
				balance--;
				if(balance == -1) {
					return false;
				}
			}
		}
		
		return true;
	}
}
```