# Number of Islands

[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/530/week-3/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/530/week-3/)
~~~
dfs를 이용해 섬의 개수를 세는 문제
~~~

```java
class Solution {

	static int W;
	static int H;
	static int[] dy = { -1, 0, 1, 0 };
	static int[] dx = { 0, 1, 0, -1 };
	static boolean visited[][];

	public int numIslands(char[][] grid) {
		H = grid.length;
        if(H == 0){
            return 0;
        }
		W = grid[0].length;
		visited = new boolean[H][W];
		int answer = 0;

		for (int y = 0; y < H; y++) {
			for (int x = 0; x < W; x++) {
				if(grid[y][x] == '1' && !visited[y][x]) {
					visited[y][x] = true;
					solve(grid, y, x);
					answer++;
				}
			}
		}
		System.out.println(answer);
		return answer;
	}

	private void solve(char[][] grid, int y, int x) {

		for (int i = 0; i < 4; i++) {
			int ny = y + dy[i];
			int nx = x + dx[i];
			if (ny < 0 || ny >= H || nx < 0 || nx >= W || visited[ny][nx] || grid[ny][nx] == '0') {
				continue;
			}

			visited[ny][nx] = true;
			solve(grid, ny, nx);
		}

	}
}
```