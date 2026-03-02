# Find Largest Value in Each Tree Row

---

## Problem Links

- LeetCode: https://leetcode.com/problems/find-largest-value-in-each-tree-row/
- GeeksforGeeks: https://www.geeksforgeeks.org/largest-value-level-binary-tree/

---

## Problem Description

Given the root of a binary tree, return an array of the largest value in each row of the tree.

Each row corresponds to a level in the tree.

The result should contain one maximum value per level.

---

## Intuition

This problem is a variation of level order traversal (BFS).

At each level:
- Multiple nodes may exist.
- We need to compute the maximum value among them.

So during level order traversal:
- Traverse level by level.
- Maintain a variable to track the maximum value for the current level.
- After processing the level, add that maximum to the result.

---

## Algorithm

1. If root is NULL, return empty list.
2. Create a queue and push the root.
3. While queue is not empty:
   - Let levelSize = number of nodes in the current level.
   - Initialize maxVal = negative infinity.
   - For i from 0 to levelSize - 1:
     - Pop node from queue.
     - Update maxVal = max(maxVal, node value).
     - Push left child if exists.
     - Push right child if exists.
   - Append maxVal to result.
4. Return result.

---

## Dry Run Example

Input Tree:

```
        1
       / \
      3   2
     / \     \
    5   3     9
```

Level 1:
Nodes: [1]  
Max: 1

Level 2:
Nodes: [3, 2]  
Max: 3

Level 3:
Nodes: [5, 3, 9]  
Max: 9

Output:
[1, 3, 9]

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
    vector<int> largestValues(TreeNode* root) {
        if (!root) return {};
        
        vector<int> result;
        queue<TreeNode*> q;
        q.push(root);
        
        while (!q.empty()) {
            int levelSize = q.size();
            int maxVal = INT_MIN;
            
            for (int i = 0; i < levelSize; ++i) {
                TreeNode* current = q.front();
                q.pop();
                
                maxVal = max(maxVal, current->val);
                
                if (current->left) q.push(current->left);
                if (current->right) q.push(current->right);
            }
            
            result.push_back(maxVal);
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
    def largestValues(self, root):
        if not root:
            return []

        result = []
        queue = deque([root])

        while queue:
            level_size = len(queue)
            max_val = float('-inf')

            for _ in range(level_size):
                node = queue.popleft()
                max_val = max(max_val, node.val)

                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

            result.append(max_val)

        return result
```

</details>

---

<details>
<summary><strong>JavaScript</strong></summary>

```javascript
var largestValues = function(root) {
    if (!root) return [];

    const result = [];
    const queue = [root];

    while (queue.length > 0) {
        const levelSize = queue.length;
        let maxVal = -Infinity;

        for (let i = 0; i < levelSize; i++) {
            const node = queue.shift();
            maxVal = Math.max(maxVal, node.val);

            if (node.left) queue.push(node.left);
            if (node.right) queue.push(node.right);
        }

        result.push(maxVal);
    }

    return result;
};
```

</details>

---

## Tags

`Tree` `Binary Tree` `BFS` `Level Order` `Maximum per Level`

---

## Variations to Practice

- Binary Tree Right Side View  
- Binary Tree Level Order Traversal  
- Zigzag Level Order Traversal  
- Average of Levels in Binary Tree  