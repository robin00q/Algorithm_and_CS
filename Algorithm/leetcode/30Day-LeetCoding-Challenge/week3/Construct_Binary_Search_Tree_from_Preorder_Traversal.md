# Construct Binary Search Tree from Preorder Traversal

[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/530/week-3/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/530/week-3/)
~~~
Preorder의 순서를 보고 Tree를 구성하는 문제
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
    public TreeNode bstFromPreorder(int[] preorder) {
        if(preorder.length == 0){
            return null;
        }
        
        int value = preorder[0];
        
        TreeNode tNode = new TreeNode(value);
        
        List<Integer> small = new ArrayList<Integer>();
        List<Integer> big = new ArrayList<Integer>();
        for(int i = 1 ; i < preorder.length ; i++){
            if(value > preorder[i]){
                small.add(preorder[i]);
            } else {
                big.add(preorder[i]);
            }
        }
        int[] left = small.stream().mapToInt(Integer::intValue).toArray();
        tNode.left = bstFromPreorder(left);
        
        int[] right = big.stream().mapToInt(Integer::intValue).toArray();
        tNode.right = bstFromPreorder(right);
        
        return tNode;
    }
}
```