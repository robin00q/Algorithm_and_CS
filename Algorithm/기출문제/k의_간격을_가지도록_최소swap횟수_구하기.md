# k의 간격을 가지도록 최소 swap 구하기

~~~
예를 들어 2, 3, 4, 5, 1 인 배열이 있고, 최소 간격이 2여야 한다고 하면

2와 5를 바꿔 5, 3, 4, 2, 1로 만들어 모든 칸의 간격이 2 이하이기 때문에 합격이다.

int[] numbers = {배열값}
int k = {최소간격}

인 경우의 답을 구하는법은 완전탐색으로 구한다.
~~~

```java
import java.util.Arrays;

class Solution {
	static int ans = Integer.MAX_VALUE;

	public int solution(int[] n, int k) {

		int[] copied = Arrays.copyOf(n, n.length);
		Arrays.sort(copied);
		if(!isValid(copied,k)) {
			return -1;
		}
		
		solve(n, k, 0, 0);
		if (n.length == 1) {
			return 0;
		}
		System.out.println(ans);

		return ans;
	}

	private void solve(int[] n, int k, int start, int depth) {
		for (int i = start; i < n.length; i++) {
			for (int j = i + 1; j < n.length; j++) {
				int[] copied = Arrays.copyOf(n, n.length);
				swap(copied, i, j);
				solve(copied, k, i + 1, depth + 1);
			}
		}
		if (isValid(n, k)) {
			ans = Math.min(depth, ans);
		}

	}

	private boolean isValid(int[] n, int k) {
		for (int i = 1; i < n.length; i++) {
			if (Math.abs(n[i] - n[i - 1]) > k) {
				return false;
			}
		}
		return true;
	}

	private void swap(int[] copied, int i, int pos) {
		int temp = copied[i];
		copied[i] = copied[pos];
		copied[pos] = temp;

	}

}

public class programmers {
	public static void main(String[] args) {
		Solution sol = new Solution();

		int[] numbers = { 2, 3, 4, 5, 1 };
		int K = 2;

		sol.solution(numbers, K);

	}
}
```