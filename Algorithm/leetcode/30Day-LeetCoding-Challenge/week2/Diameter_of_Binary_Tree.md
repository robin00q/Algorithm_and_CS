# Diameter of Binary Tree

[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/529/week-2/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/529/week-2/)
~~~
트리 좌, 우의 최대의 길이를 찾는 문제


]
~~~

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */

class Node {
    int l;
    int r;
    Node(int l, int r){
        this.l = l;
        this.r = r;
    }
}

class Solution {
    public int diameterOfBinaryTree(TreeNode root) {
        
        Node ans = search(root);
        
        return ans.l;
    }
    
    public Node search(TreeNode root) {
        if(root == null){
            return new Node(0, 0);
        }
        
        Node left = search(root.left);
        Node right = search(root.right);
        
        int diam = Math.max(left.l, right.l);
        diam = Math.max(diam, left.r + right.r);
        
        return new Node(diam, Math.max(left.r, right.r) + 1);
        
    }
}
```