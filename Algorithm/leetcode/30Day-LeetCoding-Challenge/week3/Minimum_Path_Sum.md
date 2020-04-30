# Minimum Path Sum

[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/530/week-3/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/530/week-3/)
~~~
좌측 제일 위에서 우측 제일 아래까지의 최소 cost를 찾는 문제

well known dp problem!
~~~

```java
class Solution {
	public int minPathSum(int[][] grid) {
		int H = grid.length;
		int W = grid[0].length;
		final int MAX = 987654321;

		int[][] dp = new int[H][W];
		dp[0][0] = grid[0][0];

		for (int y = 0; y < H; y++) {
			for (int x = 0; x < W; x++) {
				if (y == 0 && x == 0) {
					continue;
				}
				int fromLeft = x - 1 >= 0 ? dp[y][x - 1] : MAX;
				int fromTop = y - 1 >= 0 ? dp[y - 1][x] : MAX;
				dp[y][x] = Math.min(fromLeft, fromTop) + grid[y][x];
			}
		}
		System.out.println(dp[H - 1][W - 1]);
		return dp[H - 1][W - 1];
	}
}
```