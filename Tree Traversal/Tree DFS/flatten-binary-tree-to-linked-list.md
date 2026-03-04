# Flatten Binary Tree to Linked List

---

## Problem Links

- LeetCode: https://leetcode.com/problems/flatten-binary-tree-to-linked-list/
- GeeksforGeeks: https://www.geeksforgeeks.org/flatten-a-binary-tree-into-linked-list/

---

## Problem Description

Given the root of a binary tree, flatten the tree into a linked list in-place.

The linked list should follow the same order as the preorder traversal of the binary tree.

Requirements:

- The left child of every node should be `NULL`.
- The right child should point to the next node in preorder traversal.

Example structure after flattening:

```
1
 \
  2
   \
    3
     \
      4
```

---

## Key Observation

Preorder traversal order is:

```
Root → Left → Right
```

The flattened structure should follow exactly this order.

Instead of storing nodes in a list, we rearrange pointers directly inside the tree.

---

## Intuition

For each node:

1. If the node has a left subtree:
   - Find the rightmost node of the left subtree.
2. Attach the original right subtree to this rightmost node.
3. Move the left subtree to the right side.
4. Set the left pointer to `NULL`.

This process preserves preorder ordering.

Then move to the next node using the right pointer.

This approach resembles a **modified Morris traversal** and avoids recursion or extra memory.

---

## Algorithm

1. Initialize `curr = root`.
2. While `curr` is not NULL:
   - If `curr->left` exists:
     - Find the rightmost node of the left subtree.
     - Attach `curr->right` to that node.
     - Move left subtree to the right side.
     - Set `curr->left = NULL`.
   - Move `curr = curr->right`.
3. Continue until all nodes are processed.

---

## Dry Run Example

Input Tree:

```
        1
       / \
      2   5
     / \   \
    3   4   6
```

Step 1:

Move left subtree of 1 to right:

```
1
 \
  2
 / \
3   4
     \
      5
       \
        6
```

Final flattened tree:

```
1 -> 2 -> 3 -> 4 -> 5 -> 6
```

---

## Time and Space Complexity

Time Complexity: O(N)

Each node is visited at most twice.

Space Complexity: O(1)

No recursion or auxiliary data structures are used.

---

## Implementation (Iterative Pointer Manipulation)

<details>
<summary><strong>C++</strong></summary>

```cpp
class Solution {
public:
    void flatten(TreeNode* root) {
        TreeNode* curr = root;

        while (curr) {
            if (curr->left) {

                TreeNode* prev = curr->left;

                while (prev->right) {
                    prev = prev->right;
                }

                prev->right = curr->right;
                curr->right = curr->left;
                curr->left = nullptr;
            }

            curr = curr->right;
        }
    }
};
```

</details>

---

<details>
<summary><strong>Python</strong></summary>

```python
class Solution:
    def flatten(self, root):

        curr = root

        while curr:
            if curr.left:
                prev = curr.left

                while prev.right:
                    prev = prev.right

                prev.right = curr.right
                curr.right = curr.left
                curr.left = None

            curr = curr.right
```

</details>

---

<details>
<summary><strong>JavaScript</strong></summary>

```javascript
var flatten = function(root) {

    let curr = root;

    while (curr) {

        if (curr.left) {

            let prev = curr.left;

            while (prev.right) {
                prev = prev.right;
            }

            prev.right = curr.right;
            curr.right = curr.left;
            curr.left = null;
        }

        curr = curr.right;
    }
};
```

</details>

---

## Tags

`Tree` `Binary Tree` `Preorder` `Morris Traversal` `Pointer Manipulation`

---

## Variations to Practice

- Binary Tree Preorder Traversal  
- Construct Binary Tree from Traversals  
- Serialize and Deserialize Binary Tree  
- Convert BST to Sorted Doubly Linked List  

---