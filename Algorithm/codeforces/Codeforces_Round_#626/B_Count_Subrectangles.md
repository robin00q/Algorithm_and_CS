# B. Count Subrectangles

[https://codeforces.com/contest/1323/problem/B](https://codeforces.com/contest/1323/problem/B)

~~~
n*m 행렬에서 rectangle의 개수를 세는 문제
~~~
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;
import java.util.StringTokenizer;

public class Main {
	
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static Scanner sc = new Scanner(System.in);
	static StringTokenizer st;
	
	public static void main(String[] args) {
		
		int n = sc.nextInt();
		int m = sc.nextInt();
		long k = sc.nextInt();
		int[] a = new int[n];
		int[] b = new int[m];
		
		for(int i = 0 ; i < n ; i++) {
			a[i] = sc.nextInt();
		}
		for(int i = 0 ; i < m ; i++) {
			b[i] = sc.nextInt();
		}
		
		int[] lA = gao(a);
		int[] lB = gao(b);
		
		
		long answer = 0;
		int until = Math.max(n, m);
		for(long i = 1 ; i <= until ; i++) {
			if(k % i == 0 && i <= n && k/i <= m) {
				answer += (long)lA[(int) i] * (long)lB[(int) (k/i)];
			}
		}
		
		System.out.println(answer);
		
	}

	private static int[] gao(int[] arr) {
		
		int size = arr.length;
		int ret[] = new int[size+1];
		
		for(int i = 0 ; i < size ; i++) {
			if(arr[i] == 0) {
				continue;
			}
			
			int count = i;
			while(count < size && arr[count] == 1) {
				count++;
			}
			
			int len = count - i;
			
			for(int j = 1 ; j <= len ; j++) {
				ret[j] += len - j + 1;
			}
			i = count;
		}
		
		return ret;
	}

}

```