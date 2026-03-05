# Validate Binary Search Tree

---

## Problem Links

- LeetCode: https://leetcode.com/problems/validate-binary-search-tree/
- GeeksforGeeks: https://www.geeksforgeeks.org/check-if-a-binary-tree-is-bst-simple-and-efficient/

---

## Problem Description

Given the root of a binary tree, determine whether it is a valid Binary Search Tree (BST).

A valid BST must satisfy the following conditions:

1. The left subtree of a node contains only nodes with values **strictly less than** the node's value.
2. The right subtree of a node contains only nodes with values **strictly greater than** the node's value.
3. Both the left and right subtrees must also be valid BSTs.

---

## Example

Valid BST:

```
      2
     / \
    1   3
```

Output:

```
true
```

Invalid BST:

```
      5
     / \
    1   4
       / \
      3   6
```

Output:

```
false
```

Explanation:  
Node `3` is in the right subtree of `5`, but it is smaller than `5`, which violates the BST property.

---

## Intuition

A common mistake is checking only the immediate children of a node.  
However, BST rules apply to the **entire subtree**, not just direct children.

For example:

```
      5
     / \
    4   6
       / \
      3   7
```

Even though `3 < 6`, it is still invalid because `3` is in the right subtree of `5`.

To solve this correctly, we maintain a **valid range** for each node.

- Every node must lie within a valid `(min, max)` range.
- For the root, the range is `(-∞, +∞)`.
- For the left child, the range becomes `(min, root->val)`.
- For the right child, the range becomes `(root->val, max)`.

---

## Algorithm

1. Define a recursive function with parameters:
   - current node
   - minimum allowed value
   - maximum allowed value

2. If the node is NULL, return `true`.

3. Check if the node value violates the range:

```
node->val <= min OR node->val >= max
```

If true, return `false`.

4. Recursively validate:
   - Left subtree with updated max bound.
   - Right subtree with updated min bound.

5. Return true only if both subtrees are valid.

---

## Dry Run

Tree:

```
      5
     / \
    1   4
       / \
      3   6
```

Step 1:

```
Root = 5
Range = (-∞, +∞)
```

Step 2:

```
Node = 4
Range = (5, +∞)
```

Node `4` violates the rule because `4 < 5`.

Result:

```
false
```

---

## Time and Space Complexity

Time Complexity: O(N)

Each node is visited exactly once.

Space Complexity: O(H)

Where H is the height of the tree due to recursion stack.

Worst case (skewed tree): O(N)

---

## Implementation (DFS with Range Validation)

<details>
<summary><strong>C++</strong></summary>

```cpp
class Solution {
public:
    bool validate(TreeNode* root, long minVal, long maxVal) {
        if (!root) return true;

        if (root->val <= minVal || root->val >= maxVal)
            return false;

        return validate(root->left, minVal, root->val) &&
               validate(root->right, root->val, maxVal);
    }

    bool isValidBST(TreeNode* root) {
        return validate(root, LONG_MIN, LONG_MAX);
    }
};
```

</details>

---

<details>
<summary><strong>Python</strong></summary>

```python
class Solution:
    def isValidBST(self, root):

        def validate(node, minVal, maxVal):
            if not node:
                return True

            if node.val <= minVal or node.val >= maxVal:
                return False

            return validate(node.left, minVal, node.val) and \
                   validate(node.right, node.val, maxVal)

        return validate(root, float('-inf'), float('inf'))
```

</details>

---

<details>
<summary><strong>JavaScript</strong></summary>

```javascript
var isValidBST = function(root) {

    function validate(node, minVal, maxVal) {
        if (!node) return true;

        if (node.val <= minVal || node.val >= maxVal)
            return false;

        return validate(node.left, minVal, node.val) &&
               validate(node.right, node.val, maxVal);
    }

    return validate(root, -Infinity, Infinity);
};
```

</details>

---

## Tags

`Tree` `Binary Tree` `BST` `DFS` `Recursion`

---

## Variations to Practice

- Inorder Traversal of BST  
- Lowest Common Ancestor in BST  
- Insert into a Binary Search Tree  
- Delete Node in a BST