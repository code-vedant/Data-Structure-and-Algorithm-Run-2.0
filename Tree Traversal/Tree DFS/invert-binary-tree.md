# Invert Binary Tree

---

## Problem Links

- LeetCode: https://leetcode.com/problems/invert-binary-tree/
- GeeksforGeeks: https://www.geeksforgeeks.org/mirror-tree/

---

## Problem Description

Given the root of a binary tree, invert the tree and return its root.

Inverting a binary tree means swapping the left and right children of every node in the tree.

---

## Example

Original Tree:

```
        4
       / \
      2   7
     / \ / \
    1  3 6  9
```

After Inversion:

```
        4
       / \
      7   2
     / \ / \
    9  6 3  1
```

---

## Intuition

To invert a binary tree:

- Swap the left and right children of each node.
- Recursively apply the same operation to the left and right subtrees.

This is a classic recursion problem where the operation at each node is simple:

1. Swap children
2. Recurse into both subtrees

---

## Algorithm

1. If the current node is `NULL`, return `NULL`.
2. Swap the left and right child pointers.
3. Recursively call the function on:
   - the left subtree
   - the right subtree
4. Return the root.

---

## Dry Run

Tree:

```
    2
   / \
  1   3
```

Step 1: Swap children of 2

```
    2
   / \
  3   1
```

Step 2: Recursively process nodes 3 and 1 (they are leaves).

Final result:

```
    2
   / \
  3   1
```

---

## Time and Space Complexity

Time Complexity: O(N)

Every node in the tree is visited once.

Space Complexity: O(H)

Where H is the height of the tree due to recursion stack.

Worst case (skewed tree): O(N)

---

## Implementation (DFS Recursion)

<details>
<summary><strong>C++</strong></summary>

```cpp
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if(!root) return NULL;
        
        TreeNode* temp = root->left;
        root->left = root->right;
        root->right = temp;

        invertTree(root->left);
        invertTree(root->right);

        return root;
    }
};
```

</details>

---

<details>
<summary><strong>Python</strong></summary>

```python
class Solution:
    def invertTree(self, root):
        if not root:
            return None

        root.left, root.right = root.right, root.left

        self.invertTree(root.left)
        self.invertTree(root.right)

        return root
```

</details>

---

<details>
<summary><strong>JavaScript</strong></summary>

```javascript
var invertTree = function(root) {
    if (!root) return null;

    let temp = root.left;
    root.left = root.right;
    root.right = temp;

    invertTree(root.left);
    invertTree(root.right);

    return root;
};
```

</details>

---

## Tags

`Tree` `Binary Tree` `DFS` `Recursion` `Tree Transformation`

---

## Variations to Practice

- Symmetric Tree  
- Same Tree  
- Binary Tree Level Order Traversal  
- Binary Tree Right Side View  

---