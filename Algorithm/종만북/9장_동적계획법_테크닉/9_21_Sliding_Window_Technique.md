# 종만북 9.21 Sliding Window Technique

[https://algospot.com/judge/problem/read/TRIANGLEPATH](https://algospot.com/judge/problem/read/TRIANGLEPATH)
~~~
해당 문제에서 DP를 사용 할 경우 sliding window technique을 사용할 수 있다.

- solve() 함수에서 cache를 사용할 경우 행을 2개만 준 뒤 %2를 하는 형식으로 풀면 
  메모리를 2개의 행만 쓰면서 처리할 수 있다는 장점이 있다.

- 재귀호출 dp에서는 사용이 불가능하다.
~~~
```java
package algospot;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Scanner;
import java.util.StringTokenizer;

class Solution {
	
	private static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	private static Scanner sc = new Scanner(System.in);
	private static StringTokenizer st;
	
	private static int[][] triangle;
	private static int[][] cache;
	
	public static void solution() {
		
		int iterator = sc.nextInt();
		
		for(int i = 0 ; i < iterator ; i++) {
			solve();
		}
	}

	private static void solve() {
		
		int size = sc.nextInt();
		
		triangle = new int[size][size];
		cache = new int[2][size];
		
		for(int i = 0 ; i < size ; i++) {
			for(int j = 0 ; j <= i ; j++) {
				triangle[i][j] = sc.nextInt();
			}
		}
		
		for(int i = 0 ; i < size ; i++) {
			cache[(size-1)%2][i] = triangle[size-1][i];
		}
		
		for(int y = size-2 ; y >= 0 ; y--) {
			for(int x = 0 ; x <= y ; x++) {
				cache[y%2][x] = Math.max(cache[(y+1)%2][x] + triangle[y][x], cache[(y+1)%2][x+1] + triangle[y][x]);
			}
		}
		System.out.println(cache[0][0]);
	}
}

public class Main {
	public static void main(String[] args) throws NumberFormatException, IOException {
		
		Solution.solution();
	}
}
```