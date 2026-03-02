# Maximum Level Sum of a Binary Tree

---

## Problem Links

- LeetCode: https://leetcode.com/problems/maximum-level-sum-of-a-binary-tree/
- GeeksforGeeks: https://www.geeksforgeeks.org/level-maximum-sum-binary-tree/

---

## Problem Description

Given the root of a binary tree, return the level (1-indexed) that has the maximum sum of node values.

If multiple levels have the same maximum sum, return the smallest level number.

A level refers to all nodes at the same depth in the tree.

---

## Intuition

This problem is a direct extension of level order traversal (BFS).

At each level:
- Compute the total sum of all nodes.
- Compare it with the maximum sum seen so far.
- Track the level number where the maximum occurs.

Since BFS processes nodes level by level naturally, it is the ideal approach for this problem.

---

## Algorithm

1. If root is NULL, return 0.
2. Initialize:
   - levelVal = negative infinity (to store maximum sum seen so far)
   - levelMax = 1 (to store the level with maximum sum)
   - level = 1 (current level counter)
3. Push root into a queue.
4. While queue is not empty:
   - Let size = number of nodes in current level.
   - Initialize val = 0 (sum of current level).
   - For i from 0 to size - 1:
     - Pop node from queue.
     - Add node value to val.
     - Push left child if exists.
     - Push right child if exists.
   - If val > levelVal:
     - Update levelVal = val.
     - Update levelMax = level.
   - Increment level.
5. Return levelMax.

---

## Dry Run Example

Input Tree:

```
        1
       / \
      7   0
     / \
    7  -8
```

Level 1:
Nodes: [1]  
Sum: 1

Level 2:
Nodes: [7, 0]  
Sum: 7

Level 3:
Nodes: [7, -8]  
Sum: -1

Maximum sum = 7 at Level 2

Output:
2

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
    int maxLevelSum(TreeNode* root) {
        if (root == nullptr) {
            return 0; 
        }

        int levelVal = INT_MIN;
        int levelMax = 1;
        int level = 1;

        queue<TreeNode*> q;
        q.push(root);

        while (!q.empty()) {
            int size = q.size();
            int val = 0;

            for (int i = 0; i < size; i++) {
                TreeNode* node = q.front();
                q.pop();

                val += node->val;

                if (node->left != nullptr)
                    q.push(node->left);
                if (node->right != nullptr)
                    q.push(node->right);
            }

            if (val > levelVal) {
                levelVal = val;
                levelMax = level;
            }

            level++;
        }

        return levelMax;
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
    def maxLevelSum(self, root):
        if not root:
            return 0

        queue = deque([root])
        max_sum = float('-inf')
        max_level = 1
        level = 1

        while queue:
            level_size = len(queue)
            level_sum = 0

            for _ in range(level_size):
                node = queue.popleft()
                level_sum += node.val

                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

            if level_sum > max_sum:
                max_sum = level_sum
                max_level = level

            level += 1

        return max_level
```

</details>

---

<details>
<summary><strong>JavaScript</strong></summary>

```javascript
var maxLevelSum = function(root) {
    if (!root) return 0;

    const queue = [root];
    let maxSum = -Infinity;
    let maxLevel = 1;
    let level = 1;

    while (queue.length > 0) {
        const size = queue.length;
        let levelSum = 0;

        for (let i = 0; i < size; i++) {
            const node = queue.shift();
            levelSum += node.val;

            if (node.left) queue.push(node.left);
            if (node.right) queue.push(node.right);
        }

        if (levelSum > maxSum) {
            maxSum = levelSum;
            maxLevel = level;
        }

        level++;
    }

    return maxLevel;
};
```

</details>

---

## Tags

`Tree` `Binary Tree` `BFS` `Level Order` `Maximum Sum`

---

## Variations to Practice

- Find Largest Value in Each Tree Row  
- Binary Tree Right Side View  
- Average of Levels in Binary Tree  
- Level Order Traversal