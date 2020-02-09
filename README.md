# Validate a Binary Search Tree(BST)


# Implementation :

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
class Solution {
    public boolean isValidBST(TreeNode root) {
        if(root == null)
            return true;
        List<Integer> inorder = new ArrayList<>();
        helper(root, inorder);
        for(int i = 1; i < inorder.size(); i++){
            if(inorder.get(i) <= inorder.get(i-1))
                return false;
        }
        return true;
    }
    
    private void helper(TreeNode root, List<Integer> list){
        if(root != null){
            helper(root.left, list);
            list.add(root.val);
            helper(root.right, list);
        }
    }
}
```
