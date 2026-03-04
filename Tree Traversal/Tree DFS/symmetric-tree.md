# Symmetric Tree

---

## Problem Links

- LeetCode: https://leetcode.com/problems/symmetric-tree/
- GeeksforGeeks: https://www.geeksforgeeks.org/symmetric-tree-tree-which-is-mirror-image-of-itself/

---

## Problem Description

Given the root of a binary tree, determine whether the tree is symmetric around its center.

A binary tree is symmetric if the left subtree is a mirror reflection of the right subtree.

Return `true` if the tree is symmetric, otherwise return `false`.

---

## Intuition

For a tree to be symmetric:

- The left subtree must be a mirror of the right subtree.
- The root values of both subtrees must match.
- The left child of one subtree must match the right child of the other subtree.

This leads to a recursive comparison of mirrored nodes.

At every step we check:

1. If both nodes are `NULL`, they are symmetric.
2. If only one node is `NULL`, the structure is different.
3. If node values differ, the tree is not symmetric.
4. Recursively compare:
   - Left child of first node with right child of second node
   - Right child of first node with left child of second node

---

## Algorithm

1. If root is NULL, return `true`.
2. Call a helper function `isMirror(left, right)`.
3. In `isMirror`:
   - If both nodes are NULL, return `true`.
   - If one node is NULL, return `false`.
   - If values differ, return `false`.
4. Recursively check:
   - `left->left` with `right->right`
   - `left->right` with `right->left`
5. Return true only if both recursive checks are true.

---

## Dry Run Example

Input Tree:

```
        1
       / \
      2   2
     / \ / \
    3  4 4  3
```

Comparison steps:

- Compare left(2) and right(2)
- Compare 3 with 3
- Compare 4 with 4

All mirrored nodes match.

Output: `true`

---

## Time and Space Complexity

Time Complexity: O(N)

Each node is visited once.

Space Complexity: O(H)

Where H is the height of the tree due to recursion stack.

Worst case: O(N) for a skewed tree.

---

## Implementation (DFS Recursion)

<details>
<summary><strong>C++</strong></summary>

```cpp
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if(!root) return true;

        return isMirror(root->left, root->right);
    }

private:
    bool isMirror(TreeNode* t1, TreeNode* t2){
        if(!t1 && !t2) return true;
        if(!t1 || !t2) return false;
        if(t1->val != t2->val) return false;

        return isMirror(t1->left, t2->right) &&
               isMirror(t1->right, t2->left);
    }    
};
```

</details>

---

<details>
<summary><strong>Python</strong></summary>

```python
class Solution:
    def isSymmetric(self, root):

        def isMirror(t1, t2):
            if not t1 and not t2:
                return True
            if not t1 or not t2:
                return False
            if t1.val != t2.val:
                return False

            return isMirror(t1.left, t2.right) and \
                   isMirror(t1.right, t2.left)

        if not root:
            return True

        return isMirror(root.left, root.right)
```

</details>

---

<details>
<summary><strong>JavaScript</strong></summary>

```javascript
var isSymmetric = function(root) {

    function isMirror(t1, t2){
        if(!t1 && !t2) return true;
        if(!t1 || !t2) return false;
        if(t1.val !== t2.val) return false;

        return isMirror(t1.left, t2.right) &&
               isMirror(t1.right, t2.left);
    }

    if(!root) return true;

    return isMirror(root.left, root.right);
};
```

</details>

---

## Tags

`Tree` `Binary Tree` `DFS` `Recursion` `Mirror`

---

## Variations to Practice

- Same Tree  
- Subtree of Another Tree  
- Balanced Binary Tree  
- Maximum Depth of Binary Tree  

---