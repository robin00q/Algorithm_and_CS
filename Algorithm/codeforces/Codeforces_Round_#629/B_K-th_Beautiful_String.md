# B. K-th Beautiful String

[https://codeforces.com/contest/1328/problem/A](https://codeforces.com/contest/1328/problem/A)

~~~
n-2부터 b가 한개씩 증가 
n-2 : 1개
n-3 : 2개
n-4 : 3개
n-5 : 4개
~~~

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.Scanner;
import java.util.StringTokenizer;

public class Main {
	public static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	public static Scanner sc = new Scanner(System.in);
	public static StringTokenizer st;

	public static void main(String[] args) throws NumberFormatException, IOException {

		int iterator = sc.nextInt();

		while ((--iterator) >= 0) {
			solve();
		}
	}

	public static void solve() {
		int n = sc.nextInt();
		int k = sc.nextInt();
		char[] str = new char[n];
		Arrays.fill(str, 'a');
		
		for(int i = n-2 ; i >= 0 ; i--) {
			if(k <= n - i - 1) {
				str[i] = 'b';
				str[n-k] = 'b';
				break;
			}
			k -= (n - i - 1);
		}
		System.out.println(String.valueOf(str));
	}

}
```