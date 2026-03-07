# House Robber III

---

## Problem Links

- LeetCode: https://leetcode.com/problems/house-robber-iii/
- GeeksforGeeks: https://www.geeksforgeeks.org/maximum-sum-nodes-binary-tree-no-two-adjacent/

---

## Problem Description

A thief is planning to rob houses arranged in the form of a **binary tree**.

Each node in the tree represents a house and contains the amount of money stored in it.

Constraint:

If two **directly connected houses** (parent and child) are robbed on the same night, the police will be alerted.

Given the root of the binary tree, return the **maximum amount of money** the thief can rob without triggering the alarm.

---

## Example

Input Tree:

```
        3
       / \
      2   3
       \   \
        3   1
```

Output:

```
7
```

Explanation:

The thief robs:

```
3 + 3 + 1 = 7
```

and skips the directly connected houses.

---

## Key Observation

For every node we have **two choices**:

1. **Rob the current house**
2. **Do not rob the current house**

If we rob the current house:

- We **cannot rob its children**
- But we can rob its grandchildren

If we do not rob the current house:

- We are free to rob its children.

This naturally leads to a **dynamic programming on trees** solution.

---

## Intuition

For each node we compute two values:

```
rob → maximum money if we rob this node
skip → maximum money if we do not rob this node
```

Transitions:

If we rob the node:

```
rob = node->val + left.skip + right.skip
```

If we skip the node:

```
skip = max(left.rob, left.skip) + max(right.rob, right.skip)
```

This ensures we never rob directly connected houses.

---

## Algorithm

1. Perform DFS traversal of the tree.
2. For each node compute:
   - `rob`
   - `skip`
3. If we rob the node:

```
rob = node->val + left.skip + right.skip
```

4. If we skip the node:

```
skip = max(left.rob, left.skip) + max(right.rob, right.skip)
```

5. Return both values to the parent.
6. Final result:

```
max(root.rob, root.skip)
```

---

## Dry Run

Tree:

```
        3
       / \
      2   3
       \   \
        3   1
```

Leaf nodes:

```
3 → rob = 3, skip = 0
1 → rob = 1, skip = 0
```

Node `2`:

```
rob = 2
skip = 3
```

Node `3` (right):

```
rob = 3
skip = 1
```

Root:

```
rob = 3 + 3 + 1 = 7
skip = 6
```

Result:

```
7
```

---

## Time and Space Complexity

Time Complexity: O(N)

Each node is processed exactly once.

Space Complexity: O(H)

Where `H` is the height of the tree due to recursion stack.

Worst case (skewed tree): O(N)

---

## Implementation (DFS + Tree DP)

<details>
<summary><strong>C++</strong></summary>

```cpp
class Solution {
public:
    pair<int,int> dfs(TreeNode* root) {
        if (!root) return {0,0};

        auto left = dfs(root->left);
        auto right = dfs(root->right);

        int rob = root->val + left.second + right.second;

        int skip = max(left.first, left.second) +
                   max(right.first, right.second);

        return {rob, skip};
    }

    int rob(TreeNode* root) {
        auto res = dfs(root);
        return max(res.first, res.second);
    }
};
```

</details>

---

<details>
<summary><strong>Python</strong></summary>

```python
class Solution:
    def rob(self, root):

        def dfs(node):
            if not node:
                return (0,0)

            left = dfs(node.left)
            right = dfs(node.right)

            rob = node.val + left[1] + right[1]

            skip = max(left) + max(right)

            return (rob, skip)

        return max(dfs(root))
```

</details>

---

<details>
<summary><strong>JavaScript</strong></summary>

```javascript
var rob = function(root) {

    function dfs(node){
        if(!node) return [0,0];

        const left = dfs(node.left);
        const right = dfs(node.right);

        const rob = node.val + left[1] + right[1];

        const skip = Math.max(left[0], left[1]) +
                     Math.max(right[0], right[1]);

        return [rob, skip];
    }

    const result = dfs(root);
    return Math.max(result[0], result[1]);
};
```

</details>

---

## Tags

`Tree` `Binary Tree` `DFS` `Dynamic Programming` `Tree DP`

---

## Variations to Practice

- House Robber I  
- House Robber II  
- Binary Tree Maximum Path Sum  
- Maximum Sum of Non-Adjacent Nodes

---