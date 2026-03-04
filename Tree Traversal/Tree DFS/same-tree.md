# Same Tree

---

## Problem Links

- LeetCode: https://leetcode.com/problems/same-tree/
- GeeksforGeeks: https://www.geeksforgeeks.org/check-if-two-trees-are-identical/

---

## Problem Description

Given the roots of two binary trees `p` and `q`, determine whether they are the same tree.

Two binary trees are considered the same if:

- They are structurally identical.
- The nodes have the same values.

Return `true` if both trees are the same, otherwise return `false`.

---

## Intuition

To determine whether two trees are identical, we must compare:

1. The current node values.
2. The structure of the left subtrees.
3. The structure of the right subtrees.

This naturally leads to a **recursive solution**.

At every step:

- If both nodes are `NULL`, the trees match at this point.
- If only one node is `NULL`, the structure differs.
- If values differ, the trees are not identical.
- Otherwise, recursively compare the left and right subtrees.

---

## Algorithm

1. If both nodes are `NULL`, return `true`.
2. If one node is `NULL` and the other is not, return `false`.
3. If the values of the nodes differ, return `false`.
4. Recursively check:
   - Left subtree of both trees.
   - Right subtree of both trees.
5. Return `true` only if both recursive checks return `true`.

---

## Dry Run Example

Tree 1:

```
    1
   / \
  2   3
```

Tree 2:

```
    1
   / \
  2   3
```

Steps:

- Compare 1 and 1 → equal
- Compare left children (2 and 2) → equal
- Compare right children (3 and 3) → equal

Result: `true`

---

## Time and Space Complexity

Time Complexity: O(N)

Where N is the number of nodes.  
Each node is visited exactly once.

Space Complexity: O(H)

Where H is the height of the tree due to recursion stack.

Worst case: O(N) for skewed tree.

---

## Implementation (DFS Recursion)

<details>
<summary><strong>C++</strong></summary>

```cpp
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if (!p && !q) return true;

        if (!p || !q || p->val != q->val) return false;

        return isSameTree(p->left, q->left) &&
               isSameTree(p->right, q->right);
    }
};
```

</details>

---

<details>
<summary><strong>Python</strong></summary>

```python
class Solution:
    def isSameTree(self, p, q):
        if not p and not q:
            return True

        if not p or not q or p.val != q.val:
            return False

        return self.isSameTree(p.left, q.left) and \
               self.isSameTree(p.right, q.right)
```

</details>

---

<details>
<summary><strong>JavaScript</strong></summary>

```javascript
var isSameTree = function(p, q) {
    if (!p && !q) return true;

    if (!p || !q || p.val !== q.val) return false;

    return isSameTree(p.left, q.left) &&
           isSameTree(p.right, q.right);
};
```

</details>

---

## Tags

`Tree` `Binary Tree` `DFS` `Recursion`

---

## Variations to Practice

- Symmetric Tree  
- Subtree of Another Tree  
- Maximum Depth of Binary Tree  
- Balanced Binary Tree  

---