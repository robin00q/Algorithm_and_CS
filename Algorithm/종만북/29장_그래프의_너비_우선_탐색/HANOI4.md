# HANOI4

[https://algospot.com/judge/problem/read/HANOI4](https://algospot.com/judge/problem/read/HANOI4)

~~~
시간초과 나는데 자바라서 나는거 같다.

int로 상태공간 만드는거 매우 중요..!
~~~

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class Main {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static Queue<Integer> q = new LinkedList<Integer>();

	public static void main(String[] args) throws IOException {
		int iterator = Integer.valueOf(br.readLine());
		while ((--iterator) >= 0) {
			int N = Integer.valueOf(br.readLine());

			int first = 0;
			int end = (int) (Math.pow(4, N) - 1);

			for (int i = 0; i < 4; i++) {
				st = new StringTokenizer(br.readLine());
				int num = Integer.valueOf(st.nextToken());
				for (int j = 0; j < num; j++) {
					int index = Integer.valueOf(st.nextToken()) - 1;
					first = set(first, index, i);
				}
			}

			System.out.println(bidir(N, first, end));
		}
	}

	private static int bidir(int discs, int begin, int end) {
		if (begin == end) {
			return 0;
		}

		int[] c = new int[1 << (2*discs)];

		q.clear();

		q.add(begin);
		c[begin] = 1;
		q.add(end);
		c[end] = -1;

		while (!q.isEmpty()) {
			int here = q.poll();
			int cost = c[here];
			
			int[] top = { -1, -1, -1, -1 };

			for (int i = discs - 1; i >= 0; i--) {
				top[get(here, i)] = i;
			}

			for (int i = 0; i < 4; i++) {
				if (top[i] == -1) {
					continue;
				}
				for (int j = 0; j < 4; j++) {
					if (i != j && (top[j] == -1 || top[j] > top[i])) {
						int there = set(here, top[i], j);
						if (c[there] == 0) {
							c[there] = cost < 0 ? cost - 1 : cost + 1;
							q.add(there);
						} else if ((c[there] < 0 && cost > 0) || (cost < 0 && c[there] > 0)) {
							return Math.abs(c[there]) + Math.abs(cost) - 1;
						}
					}
				}
			}
		}

		return -1;
	}

	private static int get(int state, int index) {
		return 3 & (state >> (index * 2));
	}

	private static int set(int state, int index, int value) {
		return (state & ~(3 << (index * 2))) | (value << (index * 2));
	}

}
```