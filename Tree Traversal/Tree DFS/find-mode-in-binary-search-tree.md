# Find Mode in Binary Search Tree

---

## Problem Links

- LeetCode: https://leetcode.com/problems/find-mode-in-binary-search-tree/
- GeeksforGeeks: https://www.geeksforgeeks.org/find-mode-in-binary-search-tree/

---

## Problem Description

Given the root of a Binary Search Tree (BST) that may contain duplicate values, return all the **mode(s)** in the tree.

The **mode** is the value that appears most frequently.

If multiple values have the same highest frequency, return all of them in any order.

BST definition for this problem:

- The left subtree contains values **less than or equal to** the node.
- The right subtree contains values **greater than or equal to** the node.
- Both subtrees must also be valid BSTs.

---

## Example

Input Tree:

```
    1
     \
      2
     /
    2
```

Output:

```
[2]
```

Explanation:

Value frequencies:

```
1 → 1 time
2 → 2 times
```

Mode = `2`

---

## Key Observation

Inorder traversal of a BST produces values in **sorted order**.

Example BST:

```
        3
       / \
      2   4
     /
    1
```

Inorder traversal:

```
1, 2, 3, 4
```

When duplicates exist, they appear **next to each other** in the traversal.

This allows us to count occurrences efficiently.

---

## Intuition

We perform **inorder traversal** and track:

- `prev` → previous value visited
- `count` → current frequency of the value
- `maxCount` → highest frequency seen
- `result` → list of modes

During traversal:

1. If the current value equals the previous value → increase count.
2. Otherwise → reset count to 1.
3. If `count > maxCount`:
   - update `maxCount`
   - reset result list
4. If `count == maxCount`:
   - add value to result.

---

## Algorithm

1. Initialize:
   - `prev = NULL`
   - `count = 0`
   - `maxCount = 0`
2. Perform inorder traversal.
3. For each node:
   - If `prev == node->val` → increment count.
   - Else → reset count to 1.
4. Update modes:
   - If `count > maxCount`:
     - update maxCount
     - clear result list
     - add node value
   - If `count == maxCount`:
     - add node value
5. Update `prev`.
6. Continue traversal.

---

## Dry Run

Tree:

```
       2
      / \
     1   2
```

Inorder traversal:

```
1, 2, 2
```

Counting:

```
1 → count = 1
2 → count = 1
2 → count = 2
```

Maximum frequency = 2

Result:

```
[2]
```

---

## Time and Space Complexity

Time Complexity: O(N)

Every node is visited once.

Space Complexity: O(H)

Where H is the height of the tree due to recursion stack.

Worst case (skewed tree): O(N)

---

## Implementation (DFS Inorder)

<details>
<summary><strong>C++</strong></summary>

```cpp
class Solution {
public:
    int maxCount = 0;
    int count = 0;
    TreeNode* prev = nullptr;
    vector<int> result;

    void inorder(TreeNode* root) {
        if (!root) return;

        inorder(root->left);

        if (prev && prev->val == root->val)
            count++;
        else
            count = 1;

        if (count > maxCount) {
            maxCount = count;
            result.clear();
            result.push_back(root->val);
        }
        else if (count == maxCount) {
            result.push_back(root->val);
        }

        prev = root;

        inorder(root->right);
    }

    vector<int> findMode(TreeNode* root) {
        inorder(root);
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
    def findMode(self, root):

        self.prev = None
        self.count = 0
        self.maxCount = 0
        self.result = []

        def inorder(node):
            if not node:
                return

            inorder(node.left)

            if self.prev and self.prev.val == node.val:
                self.count += 1
            else:
                self.count = 1

            if self.count > self.maxCount:
                self.maxCount = self.count
                self.result = [node.val]
            elif self.count == self.maxCount:
                self.result.append(node.val)

            self.prev = node

            inorder(node.right)

        inorder(root)
        return self.result
```

</details>

---

<details>
<summary><strong>JavaScript</strong></summary>

```javascript
var findMode = function(root) {

    let prev = null;
    let count = 0;
    let maxCount = 0;
    let result = [];

    function inorder(node) {
        if (!node) return;

        inorder(node.left);

        if (prev && prev.val === node.val)
            count++;
        else
            count = 1;

        if (count > maxCount) {
            maxCount = count;
            result = [node.val];
        }
        else if (count === maxCount) {
            result.push(node.val);
        }

        prev = node;

        inorder(node.right);
    }

    inorder(root);
    return result;
};
```

</details>

---

## Tags

`Tree` `Binary Tree` `Binary Search Tree` `DFS` `Inorder Traversal` `Frequency`

---

## Variations to Practice

- Kth Smallest Element in BST  
- Validate Binary Search Tree  
- Binary Search Tree Iterator  
- Convert BST to Sorted List