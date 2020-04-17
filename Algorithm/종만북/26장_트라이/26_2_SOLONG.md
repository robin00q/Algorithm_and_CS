# 종만북 26.2 SOLONG

[https://algospot.com/judge/problem/read/SOLONG](https://algospot.com/judge/problem/read/SOLONG)
~~~
트라이 구현 문제

주의점
- 멤버변수 배열을 초기화 해준다.

- 생성자에서 배열을 Null로 만든다.
~~~
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.List;
import java.util.Scanner;
import java.util.StringTokenizer;

class Dictionary implements Comparable<Dictionary>{
	String word;
	int count;
	public Dictionary(String word, int count) {
		super();
		this.word = word;
		this.count = count;
	}
	@Override
	public int compareTo(Dictionary o) {
		if(this.count == o.count) {
			return this.word.compareTo(o.word);
		}
		return o.count - this.count;
	}
	@Override
	public String toString() {
		return "Dictionary [word=" + word + ", count=" + count + "]";
	}
}

class TrieNode {
	int first;
	int terminal;
	TrieNode[] children = new TrieNode[Main.ALPHA_LEN];
	
	public int getFirst() {
		return first;
	}

	public void setFirst(int first) {
		this.first = first;
	}

	public int getTerminal() {
		return terminal;
	}

	public void setTerminal(int terminal) {
		this.terminal = terminal;
	}

	public TrieNode[] getChildren() {
		return children;
	}

	public void setChildren(TrieNode[] children) {
		this.children = children;
	}

	public TrieNode() {
		this.first = -1;
		this.terminal = -1;
		for(int i = 0 ; i < Main.ALPHA_LEN ; i++) {
			children[i] = null;
		}
	}
	
	public void insert(String key, int id) {
		if(this.first == -1) {
			this.first = id;
		}
		if(key.isEmpty()) {
			this.terminal = id;
			return;
		}
		
		int next = (int)(key.charAt(0) - 'A');
		
		if(this.children[next] == null) {
			children[next] = new TrieNode();
		}
		children[next].insert(key.substring(1), id);
	}
	
	public TrieNode find(String key) {
		if(key.isEmpty()) {
			return this;
		}
		int next = (int)(key.charAt(0)-'A');
		if(this.children[next] == null) {
			return null;
		}
		return children[next].find(key.substring(1));
	}
	
	public int type(String key, int id) {
		if(key.isEmpty()) {
			return 0;
		}
		
		if(this.first == id) {
			return 1;
		}
		
		int next = toNumber(key);
		
		return 1 + children[next].type(key.substring(1), id);
	}
	
	public int toNumber(String key) {
		return (int)(key.charAt(0)-'A');
	}
	
	public int countKeys(TrieNode trie, String word) {
		TrieNode node = trie.find(word);
//		System.out.println(node);
		if(node == null || node.terminal == -1) {
			return word.length();
		}
		
		return trie.type(word, node.terminal);
	}

	@Override
	public String toString() {
		return "TrieNode [first=" + first + ", terminal=" + terminal + ", children=" + Arrays.toString(children) + "]";
	}
	
}

public class Main {
	public static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	public static Scanner sc = new Scanner(System.in);
	public static StringTokenizer st;

	public static final int ALPHA_LEN = 26;
	
	public static void main(String[] args) throws NumberFormatException, IOException {
		int T = Integer.parseInt(br.readLine());

		while (T-- > 0) {
			solve();
		}
	}

	private static void solve() throws NumberFormatException, IOException {

		st = new StringTokenizer(br.readLine());
		int N = Integer.parseInt(st.nextToken());
		int M = Integer.parseInt(st.nextToken());
		List<Dictionary> dicList = new ArrayList<Dictionary>();
		TrieNode rootTrie = new TrieNode();
		rootTrie.setFirst(Integer.MAX_VALUE);
		
		for(int i = 0 ; i < N ; i++) {
			st = new StringTokenizer(br.readLine());
			dicList.add(new Dictionary(st.nextToken(), Integer.parseInt(st.nextToken())));
		}
		
		Collections.sort(dicList);
		for(int i = 0 ; i < dicList.size() ; i++) {
			rootTrie.insert(dicList.get(i).word, i);
		}

		int answer = 0;
		st = new StringTokenizer(br.readLine());
		for(int i = 0 ; i < M ; i++) {
			answer += rootTrie.countKeys(rootTrie, st.nextToken());
		}
		
		System.out.println(answer + M-1);
		
	}
	

}

```