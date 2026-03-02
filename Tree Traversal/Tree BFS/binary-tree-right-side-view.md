# Binary Tree Right Side View

---

## Problem Links

- LeetCode: https://leetcode.com/problems/binary-tree-right-side-view/
- GeeksforGeeks: https://www.geeksforgeeks.org/right-view-binary-tree/

---

## Problem Description

Given the root of a binary tree, return the values of the nodes that are visible when the tree is viewed from the right side.

At each level of the tree, only the rightmost node should be included in the result.

Return a 1D array containing the visible nodes from top to bottom.

---

## Intuition

This problem is closely related to level order traversal (BFS).

At every level:
- Multiple nodes may exist.
- Only the last node in that level (rightmost node) is visible from the right side.

So during level order traversal:
- Process nodes level by level.
- The last node processed at each level is the one we store.

Alternatively, this can also be solved using DFS by prioritizing the right subtree first.

---

## Approach 1: BFS (Level Order Traversal)

We use a queue to traverse the tree level by level.

Key idea:
- For each level, process all nodes.
- The last node in that level is the rightmost node.
- Add it to the result.

---

## Algorithm (BFS)

1. If root is NULL, return empty list.
2. Create a queue and push the root.
3. While queue is not empty:
   - Let size = number of nodes in current level.
   - For i from 0 to size - 1:
     - Pop node from queue.
     - If i == size - 1:
       - Add node value to result.
     - Push left child if exists.
     - Push right child if exists.
4. Return result.

---

## Dry Run Example

Input Tree:

```
        1
       / \
      2   3
       \    \
        5    4
```

Level 1:
Nodes: [1]  
Rightmost: 1

Level 2:
Nodes: [2, 3]  
Rightmost: 3

Level 3:
Nodes: [5, 4]  
Rightmost: 4

Output:
[1, 3, 4]

---

## Time and Space Complexity

Time Complexity: O(N)  
Each node is visited exactly once.

Space Complexity: O(N)  
Queue may hold up to N nodes in worst case.

---

## Implementation (BFS)

<details>
<summary><strong>C++</strong></summary>

```cpp
class Solution {
public:
    vector<int> rightSideView(TreeNode* root) {
        vector<int> result;
        if (!root) return result;

        queue<TreeNode*> q;
        q.push(root);

        while (!q.empty()) {
            int size = q.size();

            for (int i = 0; i < size; i++) {
                TreeNode* node = q.front();
                q.pop();

                if (i == size - 1)
                    result.push_back(node->val);

                if (node->left)
                    q.push(node->left);

                if (node->right)
                    q.push(node->right);
            }
        }

        return result;
    }
};
```

</details>

---

<details>
<summary><strong>Python</strong></summary>

```python
from collections import deque

class Solution:
    def rightSideView(self, root):
        if not root:
            return []

        result = []
        queue = deque([root])

        while queue:
            size = len(queue)

            for i in range(size):
                node = queue.popleft()

                if i == size - 1:
                    result.append(node.val)

                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

        return result
```

</details>

---

<details>
<summary><strong>JavaScript</strong></summary>

```javascript
var rightSideView = function(root) {
    if (!root) return [];

    const result = [];
    const queue = [root];

    while (queue.length > 0) {
        const size = queue.length;

        for (let i = 0; i < size; i++) {
            const node = queue.shift();

            if (i === size - 1) {
                result.push(node.val);
            }

            if (node.left) queue.push(node.left);
            if (node.right) queue.push(node.right);
        }
    }

    return result;
};
```

</details>

---

## Approach 2: DFS (Right-First Traversal)

Instead of BFS, we can use DFS.

Key idea:
- Traverse right subtree first.
- If current depth equals result size, add node value.
- This ensures the first node encountered at each level is the rightmost node.

---

<details>
<summary><strong>C++ (DFS)</strong></summary>

```cpp
class Solution {
public:
    void dfs(TreeNode* root, int level, vector<int>& result) {
        if (!root) return;

        if (level == result.size())
            result.push_back(root->val);

        dfs(root->right, level + 1, result);
        dfs(root->left, level + 1, result);
    }

    vector<int> rightSideView(TreeNode* root) {
        vector<int> result;
        dfs(root, 0, result);
        return result;
    }
};
```

</details>

---

## Tags

`Tree` `Binary Tree` `BFS` `DFS` `Right View` `Level Order`

---

## Variations to Practice

- Left Side View of Binary Tree  
- Binary Tree Level Order Traversal  
- Zigzag Level Order Traversal  
- Vertical Order Traversal  