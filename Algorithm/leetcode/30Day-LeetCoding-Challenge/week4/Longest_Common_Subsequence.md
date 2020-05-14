# Longest Common Subsequence


[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/531/week-4/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/531/week-4/)
~~~
문자열 중 가장 긴 subsequence를 찾는 것

dp를 이용하여 같은 경우 1 + 이전dp[i-1][j-1];

다른경우 dp[i][j-1] dp[i-1][j]를 봐서 해결
~~~

```java
import java.util.Arrays;

class Solution {
	static int[][] dp;
	static String t1;
	static String t2;
    public int longestCommonSubsequence(String text1, String text2) {
    	dp = new int[1010][1010];
    	
    	for(int i = 0 ; i < dp.length; i++) {
    		Arrays.fill(dp[i], -1);
    	}
    	t1 = text1;
    	t2 = text2;
    	
    	int ret = solve(0, 0);
    	System.out.println(ret);

    	return ret;
    }
    
	private int solve(int i, int j) {
		if(i == t1.length() || j == t2.length()) {
			return 0;
		}
		
		if(dp[i][j] != -1) {
			return dp[i][j];
		}
		dp[i][j] = 0;
		if(t1.charAt(i) == t2.charAt(j)) {
			dp[i][j] = solve(i+1, j+1) + 1;
		} else {
			dp[i][j] = Math.max(solve(i+1, j), solve(i, j+1));
		}
		
		return dp[i][j];
		
	}
}
```