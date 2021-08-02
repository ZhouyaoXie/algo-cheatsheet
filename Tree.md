### TOC

- Tree Traversal
- Binary Search Tree

### Tree Traversal

- BFS
  - recursion
  - stack
- DFS
  - Preorder
  - Inorder
  - Postorder
  
  
### Binary Search Tree

**Definition**: A BST is a tree s.t. for every node, all nodes in its left subtree hold values strictly less than its own value, and all nodes in its right subtree hold values strictly greater than its own value.

**Facts** [(reference)](https://leetcode.com/problems/delete-node-in-a-bst/solution/)
1. Inorder traversal of a BST is an array sorted in ascending order.
2. To find the "successor" (the next node in inorder traversal of current node), go to its right child once, then go to the left as many times as possible.
3. To find the "predecesor" (the previous node in inorder traversal), go to left first then as many times as possible to the right.
4. A BST can be constructed from its inorder and preorder traversal. [(leetcode problem)](https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/)
