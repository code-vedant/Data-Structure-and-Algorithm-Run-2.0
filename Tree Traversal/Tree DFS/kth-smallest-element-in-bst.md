# Kth Smallest Element in a BST

---

## Problem Link

- LeetCode: https://leetcode.com/problems/kth-smallest-element-in-a-bst/

---

## Problem Description

Given the root of a Binary Search Tree (BST) and an integer `k`, return the **kth smallest value** (1-indexed) among all the node values in the tree.

The BST property guarantees:

- All values in the **left subtree** are smaller than the root.
- All values in the **right subtree** are greater than the root.

---

## Key Observation

Inorder traversal of a BST produces values in **sorted ascending order**.

Traversal order:

```
Left → Root → Right
```

Example BST:

```
        5
       / \
      3   6
     / \
    2   4
   /
  1
```

Inorder traversal:

```
1, 2, 3, 4, 5, 6
```

If `k = 3`, the answer is:

```
3
```

---

## Intuition

Since inorder traversal of a BST gives nodes in sorted order:

1. Perform inorder traversal.
2. Count nodes while visiting them.
3. When the count reaches `k`, return the current node value.

This allows us to find the kth smallest element without storing the entire traversal.

---

## Algorithm

1. Initialize a counter `count = 0`.
2. Perform inorder traversal.
3. For each visited node:
   - Increment `count`.
   - If `count == k`, return the node value.
4. Continue traversal until the kth element is found.

---

## Dry Run

Tree:

```
        5
       / \
      3   6
     / \
    2   4
   /
  1
```

Inorder traversal steps:

```
1 → count = 1
2 → count = 2
3 → count = 3  ← kth element
```

Output:

```
3
```

---

## Time and Space Complexity

Time Complexity: O(H + k)

- H = height of the tree.
- We only traverse until the kth element.

Space Complexity: O(H)

Due to recursion stack during traversal.

Worst case (skewed tree): O(N)

---

## Implementation (DFS Inorder)

<details>
<summary><strong>C++</strong></summary>

```cpp
class Solution {
public:
    int count = 0;
    int result = 0;

    void inorder(TreeNode* root, int k) {
        if (!root) return;

        inorder(root->left, k);

        count++;
        if (count == k) {
            result = root->val;
            return;
        }

        inorder(root->right, k);
    }

    int kthSmallest(TreeNode* root, int k) {
        inorder(root, k);
        return result;
    }
};
```

</details>

---

<details>
<summary><strong>Python</strong></summary>

```python
class Solution:
    def kthSmallest(self, root, k):

        self.count = 0
        self.result = None

        def inorder(node):
            if not node:
                return

            inorder(node.left)

            self.count += 1
            if self.count == k:
                self.result = node.val
                return

            inorder(node.right)

        inorder(root)
        return self.result
```

</details>

---

<details>
<summary><strong>JavaScript</strong></summary>

```javascript
var kthSmallest = function(root, k) {

    let count = 0;
    let result = null;

    function inorder(node) {
        if (!node) return;

        inorder(node.left);

        count++;
        if (count === k) {
            result = node.val;
            return;
        }

        inorder(node.right);
    }

    inorder(root);
    return result;
};
```

</details>

---

## Tags

`Tree` `Binary Tree` `Binary Search Tree` `DFS` `Inorder Traversal`

---

## Variations to Practice

- Binary Search Tree Iterator  
- Validate Binary Search Tree  
- Lowest Common Ancestor in BST  
- Convert BST to Sorted Array

---