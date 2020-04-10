# C. Dreamoon Likes Coloring
[https://codeforces.com/contest/1330/problem/C](https://codeforces.com/contest/1330/problem/C)
~~~
sum of l[i] < n => error();
for(int i = 1 ; i <= m ; i++){
	if(l[i] + i - 1 > n) {
		error();
	}
}
페인트 하기 위해서 처음부터 연속되지 않게 몇칸을 칠할 수 있는지 더해가며 선언한 뒤

이를 기반으로 칠하게 하면 됨
~~~
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Scanner;
import java.util.StringTokenizer;

public class Main {
	
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static Scanner sc = new Scanner(System.in);
	static StringTokenizer st;
	
	public static void main(String[] args) throws NumberFormatException, IOException {
		
		int n = sc.nextInt();
		int m = sc.nextInt();
		int[] l = new int[m+2];
		long[] suffixSum = new long[m+2];
		
		for(int i = 1 ; i <= m ; i++) {
			l[i] = sc.nextInt();
		}
		
		for(int i = 1 ; i <= m ; i++) {
			if(l[i] + i - 1 > n) {
				System.out.println(-1);
				return;
			} 
		}
		
		for(int i = m ; i > 0 ; i--) {
			suffixSum[i] = suffixSum[i+1] + (long)l[i];
		}
		if(suffixSum[1] < n) {
			System.out.println(-1);
			return;
		}
		
		for(int i = 1 ; i <= m ; i++) {
			int ans = (int) Math.max(i, (long)n-suffixSum[i]+1);
			System.out.print(ans);
			if(i != m) {
				System.out.print(" ");
			}
		}
		System.out.println();
		
	}

}
```