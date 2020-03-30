종만북 9.19 BLOCKGAME

![block](http://algospot.com/media/judge-attachments/065ff270c832fbe7dbc54af1227ddd5b/midgame.png)

문제 링크 : [https://algospot.com/judge/problem/read/BLOCKGAME](https://algospot.com/judge/problem/read/BLOCKGAME)

~~~
현 상황에서 내가 두었을 때 이길 수 있는가? 에 대한 문제

보통은 dx[4][3], dy[4][3] 으로 나눠서 푸는 과정을 반복하지만 이 문제에서는 DP를 이용한 접근을한다.
~~~
~~~
0,0 은 1<<0 
0,1 은 1<<1(0+1)
1,0 은 1<<5(1*5 + 0) 으로 접근해서 25비트의 비트와이즈를 이용하여 dp를 사용한다.

모든 3개 짜리 2개 짜리를 둘 수 있는 모든 곳을 precalc에서 계산한 뒤

재귀문을 이용해서 DP로 푼다.
~~~
~~~
turn을 줘야 하지 않나? (순서??)

마지막에 내가 뒀을 경우, 상대가 더 놓을 곳이 없다면 0을 return, 그러면 최종적으로 1이 return된다.

마지막의 한턴 전에 내가 뒀을 경우, 상대는 뒀을 것이고, 그 다음 내가 둘 곳이없어서 0을 return, 1을 return, 최종적으로 0이 return 된다.
~~~
```java
class Solution {
	private static Scanner sc = new Scanner(System.in);
	private static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	private static List<Integer> moves;
	private static byte[] cache;

	public static void solution() throws NumberFormatException, IOException {

		int iterator = Integer.parseInt(br.readLine());

		while ((--iterator) >= 0) {
			solve();
		}
	}

	private static void solve() throws IOException {
		
		int board = 0;
		
		for(int y = 0 ; y < 5 ; y++) {
			char[] input = br.readLine().toCharArray();
			for(int x = 0 ; x < 5 ; x++) {
				if(input[x] == '#') {
					board += cell(y, x);
				}
			}
		}
		
		moves = new ArrayList<Integer>();
		cache = new byte[1<<25];
		Arrays.fill(cache, (byte)-1);
		precalc();
		
		int answer = play(board);
		if(answer == 1) {
			System.out.println("WINNING");
			return;
		}
		System.out.println("LOSING");
	}

	public static void precalc() {
		for (int y = 0; y < 4; y++) {
			for (int x = 0; x < 4; x++) {
				ArrayList<Integer> cells = new ArrayList<Integer>();
				for (int dy = 0; dy < 2; ++dy) {
					for (int dx = 0; dx < 2; ++dx) {
						cells.add(cell(y + dy, x + dx));
					}
				}
				int square = cells.get(0) + cells.get(1) + cells.get(2) + cells.get(3);
				for(int i = 0 ; i < 4 ; i++) {
					moves.add(square - cells.get(i));
				}
			}
		}
		for(int i = 0 ; i < 5 ; i++) {
			for(int j = 0 ; j < 4 ; j++) {
				moves.add(cell(i, j) + cell(i, j+1));
				moves.add(cell(j, i) + cell(j+1, i));
			}
		}
	}
	
	public static byte play(int board) {
		
		if(cache[board] != -1) {
			return cache[board];
		}
		
		cache[board] = 0;
		for(int i = 0 ; i < moves.size() ; i++) {
			if((moves.get(i) & board) == 0) {
				if((play(board | moves.get(i)) == 0)) {
					cache[board] = 1;
					break;
				}
			}
		}

		return cache[board];
	}

	public static int cell(int y, int x) {
		return 1 << (y * 5 + x);
	}

}

public class Main {
	public static void main(String[] args) throws NumberFormatException, IOException {
		
		Solution.solution();
	}
}
```