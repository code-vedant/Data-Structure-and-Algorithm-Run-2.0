# Balanced Binary Tree

---

## Problem Links

- LeetCode: https://leetcode.com/problems/balanced-binary-tree/
- GeeksforGeeks: https://www.geeksforgeeks.org/how-to-determine-if-a-binary-tree-is-balanced/

---

## Problem Description

Given the root of a binary tree, determine whether it is **height-balanced**.

A binary tree is considered **height-balanced** if for every node:

```
|height(left subtree) - height(right subtree)| ≤ 1
```

In other words, the difference between the heights of the left and right subtrees of every node should not exceed 1.

---

## Example

Balanced Tree:

```
        3
       / \
      9   20
         /  \
        15   7
```

Output:

```
true
```

Unbalanced Tree:

```
        1
       /
      2
     /
    3
```

Output:

```
false
```

---

## Intuition

A straightforward solution would compute the height of each subtree separately and check the balance condition at every node.

However, that approach results in **O(N²)** complexity because heights are recalculated repeatedly.

Instead, we combine both operations:

- Compute the height of the subtree.
- Detect imbalance simultaneously.

We return `-1` whenever an unbalanced subtree is detected. This allows early termination.

---

## Algorithm

1. Define a recursive function `dfsHeight(node)`.

2. If the node is `NULL`, return `0`.

3. Recursively compute:
   - `leftHeight = dfsHeight(node->left)`
   - `rightHeight = dfsHeight(node->right)`

4. If either subtree returns `-1`, propagate `-1`.

5. If:

```
abs(leftHeight - rightHeight) > 1
```

return `-1` because the subtree is not balanced.

6. Otherwise return:

```
max(leftHeight, rightHeight) + 1
```

7. The tree is balanced if the final result is not `-1`.

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

Height calculations:

```
Node 4 → height = 1
Node 2 → height = 2
Node 3 → height = 1
Node 1 → difference = |2 - 1| = 1
```

Balanced → `true`

---

## Time and Space Complexity

Time Complexity: O(N)

Each node is visited exactly once.

Space Complexity: O(H)

Where `H` is the height of the tree due to recursion stack.

Worst case (skewed tree): O(N)

---

## Implementation (DFS Height Check)

<details>
<summary><strong>C++</strong></summary>

```cpp
class Solution {
public:
    bool isBalanced(TreeNode* root) {
        return dfsHeight(root) != -1;
    }
    
    int dfsHeight(TreeNode* root) {
        if (root == NULL) return 0;

        int leftHeight = dfsHeight(root->left);

        if (leftHeight == -1) 
            return -1;

        int rightHeight = dfsHeight(root->right);

        if (rightHeight == -1) 
            return -1;

        if (abs(leftHeight - rightHeight) > 1)  
            return -1;

        return max(leftHeight, rightHeight) + 1;
    }
};
```

</details>

---

<details>
<summary><strong>Python</strong></summary>

```python
class Solution:
    def isBalanced(self, root):

        def dfsHeight(node):
            if not node:
                return 0

            leftHeight = dfsHeight(node.left)
            if leftHeight == -1:
                return -1

            rightHeight = dfsHeight(node.right)
            if rightHeight == -1:
                return -1

            if abs(leftHeight - rightHeight) > 1:
                return -1

            return max(leftHeight, rightHeight) + 1

        return dfsHeight(root) != -1
```

</details>

---

<details>
<summary><strong>JavaScript</strong></summary>

```javascript
var isBalanced = function(root) {

    function dfsHeight(node) {
        if (!node) return 0;

        const leftHeight = dfsHeight(node.left);
        if (leftHeight === -1) return -1;

        const rightHeight = dfsHeight(node.right);
        if (rightHeight === -1) return -1;

        if (Math.abs(leftHeight - rightHeight) > 1)
            return -1;

        return Math.max(leftHeight, rightHeight) + 1;
    }

    return dfsHeight(root) !== -1;
};
```

</details>

---

## Tags

`Tree` `Binary Tree` `DFS` `Recursion` `Height`

---

## Variations to Practice

- Maximum Depth of Binary Tree  
- Minimum Depth of Binary Tree  
- Diameter of Binary Tree  
- Symmetric Tree

---