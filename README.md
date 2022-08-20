# Validate a Binary Search Tree(BST)
# https://leetcode.com/problems/validate-binary-search-tree

Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees.
 
```
Example 1:

    2
   / \
  1   3

Input: [2,1,3]
Output: true

Example 2:

    5
   / \
  1   4
     / \
    3   6

Input: [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.
```

## Incorrect Implementation :

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
    public boolean isValidBST(TreeNode root) {
        if(root == null)
            return true;
        return checkBST(root);
    }
    
    private boolean checkBST(TreeNode node) {
        if(node == null)
            return true;
        if(node.left != null && node.left.val >= node.val)
            return false;
        if(node.right != null && node.right.val <= node.val)
            return false;
        return checkBST(node.left) && checkBST(node.right);    
    }
}
```

The above implementation is incorrect and will fail.

!["Validate Binary Search Tree"](example.JPG?raw=true)


## Implementation 1 : Recursive

### Note : We have taken Long.MIN_VALUE and Long.MAX_VALUE, taking Integer.MIN_VALUE and Integer.MAX_VALUE will fail for 
inputs having node with value  -2,147,483,648 (-2^31) Integer.MIN_VALUE or 2,147,483,647 (2^31-1) Integer.MAX_VALUE.

Since we are given in the question that node values can range from Integer.MIN_VALUE (inclusive) to Integer.MAX_VALUE (inclusive).
Thats the reason we took Long.MIN_VALUE and Long.MAX_VALUE rather than Integer.MIN_VALUE and Integer.MAX_VALUE.

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
        return isValidBST(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }
    
    private boolean isValidBST(TreeNode node, long min, long max){
        if(node == null)
            return true;
        if(node.val <= min || node.val >= max)
            return false;
        return isValidBST(node.left, min, node.val) &&
               isValidBST(node.right, node.val, max);
    }
}
```



## Implementation 2 : Iterative
If given tree is a BST, then the Inorder traversal of the tree will be a strictly increasing sequence.

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

# References :
1. https://www.youtube.com/watch?v=yEwSGhSsT0U

2. https://www.youtube.com/watch?v=U9izQCtpVHc
