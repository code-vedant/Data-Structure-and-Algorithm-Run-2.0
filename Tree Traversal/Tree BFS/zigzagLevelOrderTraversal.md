# Binary Tree Zigzag Level Order Traversal

---

## Problem Links

- LeetCode: https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/
- GeeksforGeeks: https://www.geeksforgeeks.org/zigzag-tree-traversal/

---

## Problem Description

Given the root of a binary tree, return the zigzag level order traversal of its nodes' values.

Zigzag traversal means:
- Level 1: Left to right
- Level 2: Right to left
- Level 3: Left to right
- Level 4: Right to left
- And so on…

Return a 2D array where each inner array represents one level of the tree in zigzag order.

---

## Intuition

This problem is a variation of standard Level Order Traversal (BFS).

In normal level order traversal:
- Each level is processed from left to right.

In zigzag traversal:
- We alternate the direction at every level.

Key idea:
- Use BFS with a queue.
- Maintain a boolean flag `leftToRight`.
- For each level:
  - If leftToRight is true → fill normally.
  - If false → fill in reverse order.
- Toggle the direction after each level.

Instead of reversing the array at the end, we directly place elements at the correct index.

---

## Algorithm

1. If root is `nullptr`, return empty result.
2. Create a queue and push the root.
3. Initialize boolean variable `leftToRight = true`.
4. While queue is not empty:
   - Let size = number of nodes at current level.
   - Create a vector `level` of size `size`.
   - For each node in the level:
     - Pop node from queue.
     - Compute index:
       - If leftToRight → index = i
       - Else → index = size - 1 - i
     - Store node value at level[index].
     - Push left child if exists.
     - Push right child if exists.
   - Add level to result.
   - Toggle leftToRight.
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

Level 1 (Left to Right):
[1]

Level 2 (Right to Left):
[3, 2]

Level 3 (Left to Right):
[4, 5, 6]

Final Output:
[[1], [3, 2], [4, 5, 6]]

---

## Time and Space Complexity

Time Complexity: O(N)  
Each node is visited exactly once.

Space Complexity: O(N)  
Queue and result storage both require O(N) space in worst case.

---

## Implementation

<details>
<summary><strong>C++</strong></summary>

```cpp
class Solution {
public:
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        vector<vector<int>> ans;
        if (!root) return ans;

        queue<TreeNode*> q;
        q.push(root);
        bool leftToRight = true;

        while (!q.empty()) {
            int size = q.size();
            vector<int> level(size);

            for (int i = 0; i < size; i++) {
                TreeNode* node = q.front(); 
                q.pop();

                int index = leftToRight ? i : (size - 1 - i);
                level[index] = node->val;

                if (node->left) q.push(node->left);
                if (node->right) q.push(node->right);
            }

            ans.push_back(level);
            leftToRight = !leftToRight;
        }

        return ans;
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
    def zigzagLevelOrder(self, root):
        if not root:
            return []

        result = []
        queue = deque([root])
        leftToRight = True

        while queue:
            size = len(queue)
            level = [0] * size

            for i in range(size):
                node = queue.popleft()

                index = i if leftToRight else (size - 1 - i)
                level[index] = node.val

                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

            result.append(level)
            leftToRight = not leftToRight

        return result
```

</details>

---

<details>
<summary><strong>JavaScript</strong></summary>

```javascript
var zigzagLevelOrder = function(root) {
    if (!root) return [];

    const result = [];
    const queue = [root];
    let leftToRight = true;

    while (queue.length > 0) {
        const size = queue.length;
        const level = new Array(size);

        for (let i = 0; i < size; i++) {
            const node = queue.shift();

            const index = leftToRight ? i : (size - 1 - i);
            level[index] = node.val;

            if (node.left) queue.push(node.left);
            if (node.right) queue.push(node.right);
        }

        result.push(level);
        leftToRight = !leftToRight;
    }

    return result;
};
```

</details>

---

## Tags

`Tree` `Binary Tree` `BFS` `Zigzag Traversal` `Queue`

---

## Variations to Practice

- Standard Level Order Traversal  
- Reverse Level Order Traversal  
- Binary Tree Right View  
- Binary Tree Left View  
- Vertical Order Traversal  