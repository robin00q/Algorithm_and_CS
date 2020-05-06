# LRU Cache

[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/531/week-4/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/531/week-4/)
~~~
LRU 캐시를 구성하는 문제

연산마다 O(1) 복잡도여야 하므로 해당 인덱스의 위치가 어딨는 지 알아야함

이를 Node클래스로 double linked list형태로 구성하여 처리한다.
~~~

```java
import java.util.HashMap;
import java.util.Map;

class Node {
	Node prev;
	Node next;
	int k;
	int v;
	public Node(int k, int v) {
		super();
		this.k = k;
		this.v = v;
		this.prev = null;
		this.next = null;
	}	
}

class LRUCache {
	Node head;
	Node tail;
	int capacity;
	Map<Integer, Node> hm;

    public LRUCache(int capacity) {
        this.head = new Node(-1, -1);
        this.tail = new Node(-1, -1);
        this.capacity = capacity;
        this.hm = new HashMap<Integer, Node>();
        join(head, tail);
    }
    
    public int get(int key) {
        Node cur = hm.get(key);
        if(cur == null) {
        	return -1;
        }
        
        erase(cur);
        pushFront(cur);
        
        return cur.v;
    }
    
    public void put(int key, int value) {
        Node cur = hm.get(key);
        if(cur != null) {
        	erase(cur);
        }
        if(capacity == hm.size()) {
        	erase(tail.prev);
        }
        if(cur == null) {
        	cur = new Node(key, value);
        }
        pushFront(new Node(key, value));
    }
    
    private void pushFront(Node cur) {
    	Node next = head.next;
    	join(cur, next);
    	join(head, cur);
		hm.put(cur.k, cur);
	}

	private void erase(Node cur) {
		cur.prev.next = cur.next;
		cur.next.prev = cur.prev;
		hm.remove(cur.k);
	}

	private void join(Node n1, Node n2) {
    	n1.next = n2;
    	n2.prev = n1;
    }
}
```