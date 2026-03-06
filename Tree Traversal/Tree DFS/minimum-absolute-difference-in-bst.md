# Minimum Absolute Difference in BST

---

## Problem Links

- LeetCode: https://leetcode.com/problems/minimum-absolute-difference-in-bst/

---

## Problem Description

Given the root of a Binary Search Tree (BST), return the **minimum absolute difference** between the values of any two different nodes in the tree.

The absolute difference between two values `a` and `b` is:

```
|a - b|
```

We must find the smallest such difference among all pairs of nodes in the BST.

---

## Key Observation

Inorder traversal of a BST produces values in **sorted order**.

Traversal order:

```
Left → Root → Right
```

Example BST:

```
        4
       / \
      2   6
     / \
    1   3
```

Inorder traversal:

```
1, 2, 3, 4, 6
```

The minimum difference will always occur between **two consecutive values** in this sorted sequence.

---

## Intuition

Instead of comparing every pair of nodes (which would take O(N²)), we use inorder traversal to generate nodes in sorted order.

While traversing:

- Keep track of the **previous node value**.
- Compute the difference between the current node and the previous node.
- Update the minimum difference if a smaller value is found.

---

## Algorithm

1. Initialize:
   - `prev = NULL`
   - `minDiff = infinity`
2. Perform inorder traversal of the tree.
3. For each node:
   - If `prev` exists:
     - compute `current difference = node->val - prev`
     - update `minDiff`
4. Update `prev = node->val`
5. Continue traversal.
6. Return `minDiff`.

---

## Dry Run

Tree:

```
        4
       / \
      2   6
     / \
    1   3
```

Inorder traversal:

```
1 → 2 → 3 → 4 → 6
```

Differences:

```
2 - 1 = 1
3 - 2 = 1
4 - 3 = 1
6 - 4 = 2
```

Minimum difference:

```
1
```

---

## Time and Space Complexity

Time Complexity: O(N)

Each node is visited exactly once.

Space Complexity: O(H)

Where `H` is the height of the tree due to recursion stack.

Worst case (skewed tree): O(N)

---

## Implementation (DFS Inorder)

<details>
<summary><strong>C++</strong></summary>

```cpp
class Solution {
public:
    int minDiff = INT_MAX;
    TreeNode* prev = nullptr;

    void inorder(TreeNode* root) {
        if (!root) return;

        inorder(root->left);

        if (prev) {
            minDiff = min(minDiff, root->val - prev->val);
        }

        prev = root;

        inorder(root->right);
    }

    int getMinimumDifference(TreeNode* root) {
        inorder(root);
        return minDiff;
    }
};
```

</details>

---

<details>
<summary><strong>Python</strong></summary>

```python
class Solution:
    def getMinimumDifference(self, root):

        self.prev = None
        self.minDiff = float('inf')

        def inorder(node):
            if not node:
                return

            inorder(node.left)

            if self.prev:
                self.minDiff = min(self.minDiff, node.val - self.prev)

            self.prev = node.val

            inorder(node.right)

        inorder(root)
        return self.minDiff
```

</details>

---

<details>
<summary><strong>JavaScript</strong></summary>

```javascript
var getMinimumDifference = function(root) {

    let prev = null;
    let minDiff = Infinity;

    function inorder(node) {
        if (!node) return;

        inorder(node.left);

        if (prev !== null) {
            minDiff = Math.min(minDiff, node.val - prev);
        }

        prev = node.val;

        inorder(node.right);
    }

    inorder(root);
    return minDiff;
};
```

</details>

---

## Tags

`Tree` `Binary Tree` `Binary Search Tree` `DFS` `Inorder Traversal`

---

## Variations to Practice

- Kth Smallest Element in BST  
- Validate Binary Search Tree  
- Binary Search Tree Iterator  
- Closest Binary Search Tree Value

---