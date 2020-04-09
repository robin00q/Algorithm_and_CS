# Middle of the Linked List

[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/529/week-2/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/529/week-2/)

~~~
링크드 리스트의 중간을 리턴해주는 문제

count를 증가시키며 중간을 확인한 뒤 한번 더 진행하도록 해결
~~~

```java
class Solution {
    public ListNode middleNode(ListNode head) {
        ListNode tail = new ListNode();
        tail = head;
        int count = 1;
        while(tail.next != null) {
            tail = tail.next;
            count++;
        }
        count /= 2;
        while((count--) > 0) {
            head = head.next;
        }
        return head;
        
    }
}
```