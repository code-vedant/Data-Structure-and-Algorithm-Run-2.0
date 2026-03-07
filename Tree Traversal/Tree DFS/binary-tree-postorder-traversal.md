# Binary Tree Postorder Traversal

---

## Problem Links

- LeetCode: https://leetcode.com/problems/binary-tree-postorder-traversal/
- GeeksforGeeks: https://www.geeksforgeeks.org/postorder-traversal-of-binary-tree/

---

## Problem Description

Given the root of a binary tree, return the **postorder traversal** of its nodes' values.

Postorder traversal visits nodes in the following order:

```
Left → Right → Root
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

Postorder Traversal:

```
3 → 2 → 1
```

Output:

```
[3, 2, 1]
```

---

## Intuition

Postorder traversal processes children before the parent node.

For each node:

1. Traverse the **left subtree**.
2. Traverse the **right subtree**.
3. Visit the **current node**.

Recursion naturally fits this traversal since each subtree is also a binary tree.

---

## Algorithm

1. Create an empty list `ans`.
2. Define a recursive function `postOrder(node)`:
   - If node is `NULL`, return.
   - Recursively traverse the left subtree.
   - Recursively traverse the right subtree.
   - Add the current node value to `ans`.
3. Call the function starting from the root.
4. Return the result list.

---

## Dry Run

Tree:

```
        1
       / \
      2   3
     / \
    4   5
```

Traversal steps:

```
4 → 5 → 2 → 3 → 1
```

Result:

```
[4, 5, 2, 3, 1]
```

---

## Time and Space Complexity

Time Complexity: O(N)

Each node is visited exactly once.

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
    vector<int> postorderTraversal(TreeNode* root) {
       vector<int> ans;
       postOrder(root, ans);
       return ans;    
    }

    void postOrder(TreeNode* root, vector<int>& ans){
        if(root == nullptr)
            return;

        postOrder(root->left, ans);
        postOrder(root->right, ans);
        ans.push_back(root->val);
    }
};
```

</details>

---

<details>
<summary><strong>Python</strong></summary>

```python
class Solution:
    def postorderTraversal(self, root):
        ans = []

        def postOrder(node):
            if not node:
                return

            postOrder(node.left)
            postOrder(node.right)
            ans.append(node.val)

        postOrder(root)
        return ans
```

</details>

---

<details>
<summary><strong>JavaScript</strong></summary>

```javascript
var postorderTraversal = function(root) {
    const ans = [];

    function postOrder(node){
        if(!node) return;

        postOrder(node.left);
        postOrder(node.right);
        ans.push(node.val);
    }

    postOrder(root);
    return ans;
};
```

</details>

---

## Tags

`Tree` `Binary Tree` `DFS` `Postorder Traversal` `Recursion`

---

## Variations to Practice

- Binary Tree Preorder Traversal  
- Binary Tree Inorder Traversal  
- Maximum Depth of Binary Tree  
- Diameter of Binary Tree

---