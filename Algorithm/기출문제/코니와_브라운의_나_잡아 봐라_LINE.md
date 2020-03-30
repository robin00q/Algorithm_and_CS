# 코니와 브라운의 나 잡아 봐라

[https://engineering.linecorp.com/ko/blog/2019-firsthalf-line-internship-recruit-coding-test/](https://engineering.linecorp.com/ko/blog/2019-firsthalf-line-internship-recruit-coding-test/)
~~~
라인 코딩테스트 문제 링크에 대한 문제 풀이

BFS 내에서 +1, -1 하여 한 지점에 다시 방문할 가능성이 있으므로 (이 과정은 완전히 짝수인 경우 혹은 홀수인 경우에만 해당 되므로 brownboard 배열을 2차원으로 설정)

그냥 1차원으로 할 경우 32에 5에 방문할수도, 6에 방문할 수도 있음.

예시 : 

- 코니 11, 브라운 1인 경우

- 32 위치에 브라운은 5에 방문 , 코니는 6에 방문

- 하지만 브라운은 32를 6에도 방문할 수 있음

- 중복을 제거한 bfs를 하려다가 오히려 답을 찾을 수 없으므로 완벽한 한 점 찾기에는 예시와 같은 (홀 짝 구분(문제에 따라서)) 풀이를 해야 할 것 같음.
~~~
```java
import java.io.IOException;
import java.util.Arrays;
import java.util.LinkedList;
import java.util.Queue;

class Brown {
	int level;
	int pos;
	public Brown() {
		super();
		// TODO Auto-generated constructor stub
	}
	public Brown(int level, int pos) {
		super();
		this.level = level;
		this.pos = pos;
	}
	public int getLevel() {
		return level;
	}
	public void setLevel(int level) {
		this.level = level;
	}
	public int getPos() {
		return pos;
	}
	public void setPos(int pos) {
		this.pos = pos;
	}
}

class Solution {
	
	public static int conyboard[] = new int[200001];
	public static int brownboard[][] = new int[200001][2];
	
	public static void solution() {
		int cony = 6;
		int brown = 3;
		Queue<Brown> brownQ = new LinkedList<Brown>();
		
		Arrays.fill(conyboard, -1);
		for(int i = 0 ; i < 200001 ; i++) {
			Arrays.fill(brownboard[i], -1);
		}
		
		precalcCony(cony, 0, 0);
		
		
		brownQ.add(new Brown(0, brown));
		
		while(!brownQ.isEmpty()) {
			Brown cur = brownQ.poll();
			
			if(conyboard[cur.getPos()] == cur.getLevel()) {
				System.out.println(cur.getPos() + " " + cur.getLevel());
				break;
			}
			
			if(brownboard[cur.getPos()][cur.getLevel()%2] != -1) {
				continue;
			}
			
			brownboard[cur.getPos()][cur.getLevel()%2] = cur.getLevel();
			
			if(cur.getPos() * 2 <= 200000) {
				brownQ.add(new Brown(cur.getLevel() + 1, cur.getPos() * 2));
			}
			if(cur.getPos() + 1 <= 200000) {
				brownQ.add(new Brown(cur.getLevel() + 1, cur.getPos() + 1));
			}
			if(cur.getPos() - 1 >= 0) {
				brownQ.add(new Brown(cur.getLevel() + 1, cur.getPos() - 1));
			}
			
		}
		
	}

	

	private static void precalcCony(int cony, int count, int faster) {
		if(cony + faster > 200000) {
			return;
		}
		conyboard[cony+faster] = count;
		precalcCony(cony + faster, count+1, faster+1);
		
	}

}

public class Main {
	public static void main(String[] args) throws NumberFormatException, IOException {
		
		Solution.solution();
	}
}
```