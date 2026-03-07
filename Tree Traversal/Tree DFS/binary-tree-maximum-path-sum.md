# Binary Tree Maximum Path Sum

---

## Problem Links

- LeetCode: https://leetcode.com/problems/binary-tree-maximum-path-sum/
- GeeksforGeeks: https://www.geeksforgeeks.org/find-maximum-path-sum-in-a-binary-tree/

---

## Problem Description

Given the root of a binary tree, return the **maximum path sum** of any path in the tree.

A **path** is defined as any sequence of nodes where:

- Each pair of adjacent nodes in the sequence has an edge connecting them.
- A node can appear **at most once** in the path.

The path **does not need to pass through the root**.

The path sum is the sum of the values of the nodes along the path.

---

## Example

Input Tree:

```
        1
       / \
      2   3
```

Output:

```
6
```

Explanation:

```
2 → 1 → 3
```

Path sum:

```
2 + 1 + 3 = 6
```

---

## Key Observation

At every node we have two possible contributions:

1. The path that continues upward to the parent.
2. The path that forms a complete path passing through the node.

For each node we compute:

```
leftContribution + rightContribution + node->val
```

This represents a path **passing through the node**.

However, when returning to the parent we can only return **one side** because paths cannot split upward.

---

## Intuition

We perform DFS and compute the best contribution from each subtree.

Important rule:

```
negative contributions should be ignored
```

So we use:

```
max(0, subtreeContribution)
```

This ensures negative paths do not reduce the overall sum.

At every node we update the global maximum path sum.

---

## Algorithm

1. Initialize `maxi = -∞`.
2. Define recursive function `findMaxPath(node)`:
3. If node is NULL → return `0`.
4. Recursively compute:
   - `leftSide = max(0, findMaxPath(node->left))`
   - `rightSide = max(0, findMaxPath(node->right))`
5. Update global maximum:

```
maxi = max(maxi, leftSide + rightSide + node->val)
```

6. Return the contribution to the parent:

```
max(leftSide, rightSide) + node->val
```

7. Return `maxi`.

---

## Dry Run

Tree:

```
        -10
        /  \
       9    20
           /  \
          15   7
```

Step calculations:

```
Node 15 → contribution = 15
Node 7  → contribution = 7

Node 20 → path sum = 15 + 7 + 20 = 42
maxi = 42

Node -10 → max contribution = 20 + (-10)
```

Final result:

```
42
```

Path:

```
15 → 20 → 7
```

---

## Time and Space Complexity

Time Complexity: O(N)

Each node is visited exactly once.

Space Complexity: O(H)

Where `H` is the height of the tree due to recursion stack.

Worst case (skewed tree): O(N)

---

## Implementation (DFS)

<details>
<summary><strong>C++</strong></summary>

```cpp
class Solution {
public:
    int findMaxPath(TreeNode* root, int &maxi){
        if(root == nullptr)
            return 0;

        int leftSide = max(0, findMaxPath(root->left, maxi));    
        int rightSide = max(0, findMaxPath(root->right, maxi));

        maxi = max(maxi, leftSide + rightSide + root->val);

        return max(leftSide, rightSide) + root->val;   
    }

    int maxPathSum(TreeNode* root) {
        int maxi = INT_MIN;

        findMaxPath(root, maxi);

        return maxi;
    }
};
```

</details>

---

<details>
<summary><strong>Python</strong></summary>

```python
class Solution:
    def maxPathSum(self, root):

        self.maxi = float('-inf')

        def findMaxPath(node):
            if not node:
                return 0

            left = max(0, findMaxPath(node.left))
            right = max(0, findMaxPath(node.right))

            self.maxi = max(self.maxi, left + right + node.val)

            return max(left, right) + node.val

        findMaxPath(root)
        return self.maxi
```

</details>

---

<details>
<summary><strong>JavaScript</strong></summary>

```javascript
var maxPathSum = function(root) {

    let maxi = -Infinity;

    function findMaxPath(node){
        if(!node) return 0;

        const left = Math.max(0, findMaxPath(node.left));
        const right = Math.max(0, findMaxPath(node.right));

        maxi = Math.max(maxi, left + right + node.val);

        return Math.max(left, right) + node.val;
    }

    findMaxPath(root);
    return maxi;
};
```

</details>

---

## Tags

`Tree` `Binary Tree` `DFS` `Dynamic Programming` `Maximum Path`

---

## Variations to Practice

- Maximum Depth of Binary Tree  
- Diameter of Binary Tree  
- Balanced Binary Tree  
- Path Sum