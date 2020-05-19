# 종만북 29.2 Sorting Game

[https://algospot.com/judge/problem/read/SORTGAME](https://algospot.com/judge/problem/read/SORTGAME)


~~~
# Soring Game 자바 시간초과 
# Soring Game java 시간초과

java로 해당 문제를 종만북의 알고리즘 그대로 하면 시간 초과가 날 것.

해당 문제를 풀기 위해서 비트와이즈를 이용한 integer로 상태공간을 정의하여 푼다. (종만북 588쪽 (16장 비트와이즈 참조))

[0, 1, 2, 3, 4, 5, 6, 7]의 reverse형태들을 아래의 set함수를 이용하여 bitwise로 int변수로 바꾼다.

이를 hashmap에 저장하여 해결
~~~

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.HashMap;
import java.util.LinkedList;
import java.util.Queue;
import java.util.Scanner;
import java.util.StringTokenizer;

public class Main {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static Scanner sc = new Scanner(System.in);
	static StringTokenizer st;

	static HashMap<Integer, Integer> toSort = new HashMap<Integer, Integer>();

	public static void main(String[] args) throws IOException {
		int iterator = Integer.valueOf(br.readLine());
		for (int i = 1; i <= 8; i++) {
			precalc(i);
		}
		while ((--iterator) >= 0) {
			solve();
		}
	}

	private static void solve() throws NumberFormatException, IOException {
		int n = Integer.parseInt(br.readLine());
		int[] perm = new int[n];
		int[] fixed = new int[n];

		st = new StringTokenizer(br.readLine());
		for (int i = 0; i < n; i++) {
			perm[i] = Integer.parseInt(st.nextToken());
		}

		for (int i = 0; i < n; i++) {
			int smaller = 0;
			for (int j = 0; j < n; j++) {
				if (perm[j] < perm[i]) {
					smaller++;
				}
			}
			fixed[i] = smaller;
		}

		int ret = getState(fixed);

		System.out.println(toSort.get(ret));
	}

	private static void precalc(int n) {
		int init = 0;
		for (int i = 0; i < n; i++) {
			init = set(init, i, i);
		}

		Queue<Integer> q = new LinkedList<Integer>();
		q.add(init);
		toSort.put(init, 0);

		while (!q.isEmpty()) {
			int here = q.poll();
			int cost = toSort.get(here);

			for (int i = 0; i < n; i++) {
				for (int j = i + 1; j < n; j++) {
					int[] reversed = reverse(n, here, i, j);
					int there = getState(reversed);
					if (toSort.get(there) == null) {
						toSort.put(there, cost + 1);
						q.add(there);
					}
				}
			}
		}
	}

	private static int getState(int[] arr) {
		int state = 0;

		for (int i = 0; i < arr.length; i++) {
			state = set(state, i, arr[i]);
		}

		return state;
	}

	private static int[] reverse(int n, int state, int from, int to) {
		int[] arr = new int[n];
		int[] arr2 = new int[n];

		for (int i = 0; i < n; i++) {
			int value = get(state, i);
			arr[i] = value;
			arr2[i] = value;
		}

		int pos = to;
		for (int i = from; i <= to; i++) {
			arr[i] = arr2[pos--];
		}

		return arr;
	}

	private static int get(int state, int index) {
		return 7 & (state >> (index * 3));
	}

	private static int set(int state, int index, int value) {
		return (state & ~(7 << (index * 3))) | (value << (index * 3));
	}

}
```