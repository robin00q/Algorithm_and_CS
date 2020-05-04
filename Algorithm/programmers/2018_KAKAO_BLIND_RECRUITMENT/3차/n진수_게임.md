# n진수 게임

[https://programmers.co.kr/learn/courses/30/lessons/17687](https://programmers.co.kr/learn/courses/30/lessons/17687)

~~~
재귀호출을 이용하여 N진수의 경우 String을 추출

이후 개수를 세면서 반복
~~~

```java
class Solution {
	static int N;
	public String solution(int n, int t, int m, int p) {
		String answer = "";
		N = n;
		
		int count = 0;
		for(int i = 0 ; i <= Integer.MAX_VALUE ; i++) {
			String s = getNumString(i);
			if(i == 0) {
				s = "0";
			}
			for(int j = 0 ; j < s.length() ; j++) {
				if((count % m) == p-1){
					answer+= s.charAt(j);
				}
				if(answer.length() == t) {
					// System.out.println(answer);
					return answer;
				}
				count++;
			}
		}

		return "error";
	}

	private String getNumString(int i) {
		if(i == 0) {
			return "";
		}
		int cur = i % N;
		String curString = "" + cur;
		if(cur >= 10) {
			curString = "" + (char) ('A' + (cur-10));
		}
		return  getNumString(i/N) + curString;
	}
}
```