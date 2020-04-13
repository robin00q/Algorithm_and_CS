# Min Stack
https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/529/week-2/
~~~
스택의 구현을 푸는 문제

스택의 구현에서 min을 가지고 오는 경우 Pair를 이용해서 갱신하도록 함
~~~
```java
class Pair {
    int a;
    int b;
    public Pair(int a, int b){
        this.a = a;
        this.b = b;
    }
    public Pair(){
        super();
    }
    public int getB(){
        return b;
    }
    public int getA(){
        return a;
    }
}

class MinStack {

    Stack<Pair> mStack;
    /** initialize your data structure here. */
    public MinStack() {
        mStack = new Stack<Pair>();
    }
    
    public void push(int x) {
        if(this.mStack.size() == 0 || this.getMin() > x) {
            mStack.push(new Pair(x, x));
        } else {
            mStack.push(new Pair(x, this.getMin()));
        }
    }
    
    public void pop() {
        mStack.pop();
    }
    
    public int top() {
        return mStack.peek().getA();
    }
    
    public int getMin() {
        return mStack.peek().getB();
    }
}
```
