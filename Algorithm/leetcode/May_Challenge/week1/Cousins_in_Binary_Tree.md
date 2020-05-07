# Cousins in Binary Tree

~~~
같은 높이면서 부모가 다른 cousin을 찾는 문제

원하는 노드 2개를 찾아 부모와 depth를 list에 넣은 후 비교
~~~

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    static List<Integer> depth = new ArrayList<Integer>();
    static List<Integer> parent = new ArrayList<Integer>();
    public boolean isCousins(TreeNode root, int x, int y) {
        if(x == root.val || y == root.val){
            return false;
        }
        
        depth.clear();
        parent.clear();
        
        getParent(root, x, 0);
        getParent(root, y, 0);
        
        if(parent.get(0).intValue() == parent.get(1).intValue()){
            return false;
        }
        
        if(depth.get(0).intValue() == depth.get(1).intValue()){
            return true;
        }
        
        return false;
    }
    
    public void getParent(TreeNode root, int x, int d){
        if((root.left != null && root.left.val == x) || (root.right != null && root.right.val == x)){
            depth.add(d+1);
            parent.add(root.val);
            return;
        }
        
        if(root.left != null){
            getParent(root.left, x, d+1);
        }
        if(root.right != null){
            getParent(root.right, x, d+1);
        }
        
        return;
    }
}
```
