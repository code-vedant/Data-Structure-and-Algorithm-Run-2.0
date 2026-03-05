# Binary Tree Paths

---

## Problem Links

- LeetCode: https://leetcode.com/problems/binary-tree-paths/
- GeeksforGeeks: https://www.geeksforgeeks.org/given-a-binary-tree-print-all-root-to-leaf-paths/

---

## Problem Description

Given the root of a binary tree, return all root-to-leaf paths.

A root-to-leaf path is a sequence of nodes starting from the root node and ending at a leaf node.

A leaf node is a node that does not have any children.

The result should contain all such paths in any order.

Each path is typically represented as a string in the format:

```
node1->node2->node3
```

---

## Example

Input Tree:

```
        1
       / \
      2   3
       \
        5
```

Output:

```
["1->2->5", "1->3"]
```

Explanation:

Two root-to-leaf paths exist:

- 1 → 2 → 5
- 1 → 3

---

## Intuition

This problem requires exploring every possible root-to-leaf path.

A natural approach is **Depth First Search (DFS)**.

At each node:

1. Add the current node to the path.
2. If the node is a leaf, store the completed path.
3. Otherwise, continue exploring its left and right children.

The recursion naturally builds paths from root to leaf.

---

## Algorithm

1. If root is NULL, return an empty list.
2. Create a recursive DFS function that keeps track of the current path.
3. At each node:
   - Append the current node value to the path.
4. If the node is a leaf:
   - Add the path to the result.
5. Otherwise:
   - Recurse into the left child.
   - Recurse into the right child.
6. Return the result list.

---

## Dry Run Example

Tree:

```
        1
       / \
      2   3
       \
        5
```

Step-by-step traversal:

Path: `1`

Left branch:
```
1 -> 2
```

Continue:

```
1 -> 2 -> 5
```

Leaf reached → store `"1->2->5"`

Backtrack.

Right branch:

```
1 -> 3
```

Leaf reached → store `"1->3"`

Final Result:

```
["1->2->5", "1->3"]
```

---

## Time and Space Complexity

Time Complexity: O(N)

Each node is visited once.

Space Complexity: O(H)

Where H is the height of the tree due to recursion stack.

The output list may take additional space proportional to the number of paths.

---

## Implementation (DFS)

<details>
<summary><strong>C++</strong></summary>

```cpp
class Solution {
public:
    void dfs(TreeNode* root, string path, vector<string>& result) {
        if (!root) return;

        if (!path.empty()) {
            path += "->";
        }
        path += to_string(root->val);

        if (!root->left && !root->right) {
            result.push_back(path);
            return;
        }

        dfs(root->left, path, result);
        dfs(root->right, path, result);
    }

    vector<string> binaryTreePaths(TreeNode* root) {
        vector<string> result;
        dfs(root, "", result);
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
    def binaryTreePaths(self, root):

        result = []

        def dfs(node, path):
            if not node:
                return

            if path:
                path += "->"

            path += str(node.val)

            if not node.left and not node.right:
                result.append(path)
                return

            dfs(node.left, path)
            dfs(node.right, path)

        dfs(root, "")
        return result
```

</details>

---

<details>
<summary><strong>JavaScript</strong></summary>

```javascript
var binaryTreePaths = function(root) {

    const result = [];

    function dfs(node, path) {
        if (!node) return;

        if (path.length > 0) {
            path += "->";
        }

        path += node.val;

        if (!node.left && !node.right) {
            result.push(path);
            return;
        }

        dfs(node.left, path);
        dfs(node.right, path);
    }

    dfs(root, "");
    return result;
};
```

</details>

---

## Tags

`Tree` `Binary Tree` `DFS` `Backtracking` `Root to Leaf`

---

## Variations to Practice

- Path Sum  
- Sum Root to Leaf Numbers  
- Binary Tree Maximum Path Sum  
- Leaf Similar Trees

---