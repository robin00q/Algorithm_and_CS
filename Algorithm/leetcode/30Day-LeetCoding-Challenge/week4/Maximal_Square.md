# Maximal Square

[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/531/week-4/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/531/week-4/)
~~~
최대 넓이를 가진 사각형을 찾는 문제

dp[i][j] = Math.min(dp[i][j-1] , dp[i-1][j-1], dp[i-1][j]) + 1;
~~~

```java
class Solution {
    public int maximalSquare(char[][] matrix) {
        if(matrix.length == 0){
            return 0;
        }
        int H = matrix.length;
        int W = matrix[0].length;
        int[][] dp = new int[H+1][W+1];
        int answer = 0;
        
        for(int i = 0 ; i < H ; i++){
            for(int j = 0 ; j < W ; j++){
                if(matrix[i][j] == '1'){
                    dp[i+1][j+1] = Math.min(dp[i][j], Math.min(dp[i+1][j], dp[i][j+1]))+1;                                 answer = Math.max(answer,dp[i+1][j+1] * dp[i+1][j+1]);
                }
            }
        }
        
        return answer;
    }
}
```