# Binary Tree Level Order Traversal

---

## Problem Links

- LeetCode: https://leetcode.com/problems/binary-tree-level-order-traversal/
- GeeksforGeeks: https://www.geeksforgeeks.org/level-order-traversal-in-binary-tree/

---

## Problem Description

Given the root of a binary tree, return the level order traversal of its nodes' values.

Level order traversal means:
- Traverse the tree level by level.
- For each level, collect all nodes from left to right.

Return a 2D array where each inner array represents one level of the tree.

---

## Intuition

This problem is a classic application of Breadth First Search (BFS) on a tree.

Why BFS?

BFS naturally processes nodes level by level. A queue helps maintain the order of traversal. By processing all nodes currently in the queue before moving to the next level, we can separate each level cleanly.

Core idea:
- Push the root into a queue.
- While the queue is not empty:
  - Process all nodes currently in the queue (one level).
  - Add their children to the queue.
- Store each level separately in the result.

---

## Algorithm

1. If root is NULL, return an empty result.
2. Create an empty 2D list/vector called result.
3. Create a queue and push the root node into it.
4. While the queue is not empty:
   - Let size be the number of nodes currently in the queue.
   - Create an empty list called level.
   - Repeat size times:
     - Remove a node from the queue.
     - Add its value to level.
     - If left child exists, push it into the queue.
     - If right child exists, push it into the queue.
   - Append level to result.
5. Return result.

---

## Dry Run Example

Input Tree:

```
        1
       / \
      2   3
     / \   \
    4   5   6
```

Execution:

Initial queue: [1]

Level 1:
- Process 1
- Push 2, 3
Result: [[1]]

Level 2:
- Process 2, 3
- Push 4, 5, 6
Result: [[1], [2, 3]]

Level 3:
- Process 4, 5, 6
Result: [[1], [2, 3], [4, 5, 6]]

---

## Time and Space Complexity

Time Complexity: O(N)  
Each node is visited exactly once.

Space Complexity: O(N)  
The queue may store up to N nodes in the worst case. The output also requires O(N) space.

---

## Implementation

<details>
<summary><strong>C++</strong></summary>

```cpp
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> result;

        if (root == nullptr)
            return result;

        queue<TreeNode*> q;
        q.push(root);

        while (!q.empty()) {
            int size = q.size();
            vector<int> level;

            for (int i = 0; i < size; i++) {
                TreeNode* node = q.front();
                q.pop();

                level.push_back(node->val);

                if (node->left)
                    q.push(node->left);

                if (node->right)
                    q.push(node->right);
            }

            result.push_back(level);
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
    def levelOrder(self, root):
        if not root:
            return []

        result = []
        queue = deque([root])

        while queue:
            level_size = len(queue)
            level = []

            for _ in range(level_size):
                node = queue.popleft()
                level.append(node.val)

                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

            result.append(level)

        return result
```

</details>

---

<details>
<summary><strong>JavaScript</strong></summary>

```javascript
var levelOrder = function(root) {
    if (!root) return [];

    const result = [];
    const queue = [root];

    while (queue.length > 0) {
        const size = queue.length;
        const level = [];

        for (let i = 0; i < size; i++) {
            const node = queue.shift();
            level.push(node.val);

            if (node.left) queue.push(node.left);
            if (node.right) queue.push(node.right);
        }

        result.push(level);
    }

    return result;
};
```

</details>

---

## Tags

`Tree`  `Binary Tree` `BFS`  `Queue`   `Level Order Traversal`  

---

## Variations to Practice

- Binary Tree Zigzag Level Order Traversal  
- Reverse Level Order Traversal  
- Right View of Binary Tree  
- Left View of Binary Tree  
- Average of Levels in Binary Tree  