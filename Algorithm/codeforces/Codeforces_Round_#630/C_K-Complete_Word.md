# C. K-Complete Word

~~~
어떤 문자열이 pos + k가 항상 같으면서 palindrome인 문자열의 최소 변환횟수 반환

홀수 인 경우 (5)
pos, pos+1, pos+2, pos+1, pos 의 형태로 같아야 하기 때문에
짝수 인 경우 (6)
pos, pos+1, pos+2, pos+2, pos+1, pos 의 형태로 같아야 하기 때문에

이를 2차원 배열에 처리한 뒤 최소 변환횟수 반환

~~~

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Scanner;
import java.util.StringTokenizer;


public class Main {
	public static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	public static Scanner sc = new Scanner(System.in);
	public static StringTokenizer st;
	
	
	public static void main(String[] args) throws NumberFormatException, IOException {
		int iterator = Integer.parseInt(br.readLine());
		while((--iterator) >= 0) {
			solve();
		}
	}

	private static void solve() throws NumberFormatException, IOException {
		
		st = new StringTokenizer(br.readLine());
		
		int len = Integer.parseInt(st.nextToken());
		int k = Integer.parseInt(st.nextToken());
		int div;
		if(k % 2 == 0) {
			div = k/2;
		} else {
			div = k/2+1;
		}
		int[][] board = new int[div][26];
		
		char[] word = br.readLine().toCharArray();
		for(int i = 0 ; i < len ; i++) {
			int p = i%k;
			if(p >= div) {
				p = k - p - 1;
			}
			board[p][word[i]-'a']++;
		}
		
		int answer = 0;
		for(int i = 0 ; i < div ; i++) {
			int max = 0;
			int cur = 0;
			for(int j = 0 ; j < 26 ; j++) {
				max = Math.max(max, board[i][j]);
				cur += board[i][j];
			}
			answer += (cur-max);
		}
		
		System.out.println(answer);
	}
}
```