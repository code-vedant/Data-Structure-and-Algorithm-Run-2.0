# Binary Tree Inorder Traversal

---

## Problem Links

- LeetCode: https://leetcode.com/problems/binary-tree-inorder-traversal/
- GeeksforGeeks: https://www.geeksforgeeks.org/inorder-tree-traversal/

---

## Problem Description

Given the root of a binary tree, return the inorder traversal of its nodes' values.

In inorder traversal, nodes are visited in the following order:

```
Left → Root → Right
```

The result should be returned as a list containing the node values in this order.

---

## Example

Input Tree:

```
    1
     \
      2
     /
    3
```

Inorder Traversal:

```
1 → 3 → 2
```

Output:

```
[1, 3, 2]
```

---

## Intuition

Inorder traversal follows a simple recursive pattern:

1. Traverse the left subtree.
2. Visit the current node.
3. Traverse the right subtree.

This pattern naturally fits recursion because every subtree is itself a binary tree.

---

## Algorithm

1. Create an empty list `ans`.
2. Define a recursive function `inorder(node)`:
   - If the node is NULL, return.
   - Recursively call `inorder(node->left)`.
   - Add the node value to the result list.
   - Recursively call `inorder(node->right)`.
3. Call the function starting from the root.
4. Return the result list.

---

## Dry Run

Tree:

```
        4
       / \
      2   5
     / \
    1   3
```

Steps:

```
Visit left subtree of 4
→ Visit left subtree of 2
→ Visit 1
→ Visit 2
→ Visit 3
→ Visit 4
→ Visit 5
```

Result:

```
[1, 2, 3, 4, 5]
```

---

## Time and Space Complexity

Time Complexity: O(N)

Each node is visited exactly once.

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
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> ans;
        inorder(root, ans);
        return ans;
    }

    void inorder(TreeNode* root, vector<int>& ans) {
        if (root == nullptr)
            return;

        inorder(root->left, ans);
        ans.push_back(root->val);
        inorder(root->right, ans);
    }
};
```

</details>

---

<details>
<summary><strong>Python</strong></summary>

```python
class Solution:
    def inorderTraversal(self, root):
        ans = []

        def inorder(node):
            if not node:
                return

            inorder(node.left)
            ans.append(node.val)
            inorder(node.right)

        inorder(root)
        return ans
```

</details>

---

<details>
<summary><strong>JavaScript</strong></summary>

```javascript
var inorderTraversal = function(root) {
    const ans = [];

    function inorder(node) {
        if (!node) return;

        inorder(node.left);
        ans.push(node.val);
        inorder(node.right);
    }

    inorder(root);
    return ans;
};
```

</details>

---

## Tags

`Tree` `Binary Tree` `DFS` `Inorder Traversal` `Recursion`

---

## Variations to Practice

- Binary Tree Preorder Traversal  
- Binary Tree Postorder Traversal  
- Morris Inorder Traversal  
- Validate Binary Search Tree