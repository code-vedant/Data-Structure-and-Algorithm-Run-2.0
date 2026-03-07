# Maximum Depth of Binary Tree

---

## Problem Links

- LeetCode: https://leetcode.com/problems/maximum-depth-of-binary-tree/
- GeeksforGeeks: https://www.geeksforgeeks.org/find-the-maximum-depth-or-height-of-a-tree/

---

## Problem Description

Given the root of a binary tree, return its **maximum depth**.

The maximum depth of a binary tree is the number of nodes along the **longest path from the root node down to the farthest leaf node**.

A leaf node is a node with no children.

---

## Example

Input Tree:

```
        3
       / \
      9   20
         /  \
        15   7
```

Output:

```
3
```

Explanation:

The longest path from root to leaf is:

```
3 → 20 → 15
```

or

```
3 → 20 → 7
```

Both have length **3**.

---

## Intuition

The depth of a tree depends on the depth of its subtrees.

For every node:

```
depth(node) = 1 + max(depth(left), depth(right))
```

This means:

1. Recursively compute the depth of the left subtree.
2. Recursively compute the depth of the right subtree.
3. Take the maximum of the two.
4. Add 1 for the current node.

---

## Algorithm

1. If the node is `NULL`, return `0`.
2. Recursively compute:
   - `leftDepth = maxDepth(root->left)`
   - `rightDepth = maxDepth(root->right)`
3. Return:

```
max(leftDepth, rightDepth) + 1
```

---

## Dry Run

Tree:

```
        1
       / \
      2   3
     /
    4
```

Step-by-step:

```
Node 4 → depth = 1
Node 2 → depth = 2
Node 3 → depth = 1
Node 1 → max(2,1) + 1 = 3
```

Result:

```
3
```

---

## Time and Space Complexity

Time Complexity: O(N)

Every node is visited exactly once.

Space Complexity: O(H)

Where `H` is the height of the tree due to recursion stack.

Worst case (skewed tree): O(N)

---

## Implementation (DFS Recursion)

<details>
<summary><strong>C++</strong></summary>

```cpp
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (root == NULL) {
            return 0;
        }

        int leftDepth = maxDepth(root->left);
        int rightDepth = maxDepth(root->right);

        return max(leftDepth, rightDepth) + 1;
    }
};
```

</details>

---

<details>
<summary><strong>Python</strong></summary>

```python
class Solution:
    def maxDepth(self, root):
        if not root:
            return 0

        leftDepth = self.maxDepth(root.left)
        rightDepth = self.maxDepth(root.right)

        return max(leftDepth, rightDepth) + 1
```

</details>

---

<details>
<summary><strong>JavaScript</strong></summary>

```javascript
var maxDepth = function(root) {
    if (!root) return 0;

    const leftDepth = maxDepth(root.left);
    const rightDepth = maxDepth(root.right);

    return Math.max(leftDepth, rightDepth) + 1;
};
```

</details>

---

## Tags

`Tree` `Binary Tree` `DFS` `Recursion` `Depth`

---

## Variations to Practice

- Minimum Depth of Binary Tree  
- Balanced Binary Tree  
- Diameter of Binary Tree  
- Maximum Path Sum

---