# Strongly Connected Component

[https://www.acmicpc.net/problem/2150](https://www.acmicpc.net/problem/2150)

~~~
타잔 알고리즘을 이용한 SCC 분리
~~~

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;
import java.util.Scanner;
import java.util.Stack;
import java.util.StringTokenizer;

public class Main {
	public static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	public static Scanner sc = new Scanner(System.in);
	public static StringTokenizer st;

	public static List<Integer>[] adj;
	public static int[] sccId;
	public static int[] discovered;
	public static int sccCounter, vertexCounter;
	public static Stack<Integer> stack = new Stack<Integer>();
	public static int V;
	public static int E;
	public static List<List<Integer>> answerList = new ArrayList<List<Integer>>();

	public static void main(String[] args) throws NumberFormatException, IOException {
		tarjanSCC();
	}

	private static void tarjanSCC() throws IOException {
		st = new StringTokenizer(br.readLine());
		
		V = Integer.parseInt(st.nextToken());
		E = Integer.parseInt(st.nextToken());
		
		sccId = new int[V+1];
		discovered = new int[V+1];
		
		Arrays.fill(sccId, -1);
		Arrays.fill(discovered, -1);

		adj = new List[V+1];
		for (int i = 0; i < adj.length; i++) {
			adj[i] = new ArrayList<Integer>();
		}
		
		for(int i = 0 ; i < E ; i++) {
			st = new StringTokenizer(br.readLine());
			int u = Integer.parseInt(st.nextToken());
			int v = Integer.parseInt(st.nextToken());
			
			adj[u].add(v);
		}

		for (int i = 1; i < adj.length; i++) {
			if (discovered[i] == -1) {
				scc(i);
			}
		}
		
		Collections.sort(answerList, new Comparator<List<Integer>>() {
			@Override
			public int compare(List<Integer> o1, List<Integer> o2) {
				return o1.get(0) - o2.get(0);
			}
		});
		
		System.out.println(answerList.size());
		for(List<Integer> l : answerList) {
			for(int elem : l) {
				System.out.print(elem + " ");
			}
			System.out.println(-1);
		}
	}


	private static int scc(int here) {
		int ret = discovered[here] = vertexCounter++;

		stack.add(here);
		for (int i = 0; i < adj[here].size(); i++) {
			int there = adj[here].get(i);
			if (discovered[there] == -1) {
				ret = Math.min(ret, scc(there));
			} else if (sccId[there] == -1) {
				ret = Math.min(ret, discovered[there]);
			}
		}

		if (ret == discovered[here]) {
			List<Integer> l = new ArrayList<Integer>();
			while (true) {
				int t = stack.pop();
				l.add(t);
				sccId[t] = sccCounter;
				if (t == here) {
					break;
				}
			}
			Collections.sort(l);
			answerList.add(l);
			
			sccCounter++;
		}

		return ret;
	}

}
```