# Construct Binary Tree from Preorder and Inorder Traversal

---

## Problem Links

- LeetCode: https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/
- GeeksforGeeks: https://www.geeksforgeeks.org/construct-tree-from-given-inorder-and-preorder-traversal/

---

## Problem Description

Given two integer arrays:

- `preorder` – preorder traversal of a binary tree
- `inorder` – inorder traversal of the same binary tree

Construct and return the binary tree.

It is guaranteed that the tree contains unique values.

---

## Key Observations

Traversal properties:

Preorder traversal order:

```
Root → Left → Right
```

Inorder traversal order:

```
Left → Root → Right
```

Important insight:

- The **first element in preorder is always the root**.
- Using this root, we can split the inorder array into:
  - Left subtree
  - Right subtree

Example:

Preorder:
```
[3, 9, 20, 15, 7]
```

Inorder:
```
[9, 3, 15, 20, 7]
```

Root = `3`

In inorder:
```
[9] 3 [15,20,7]
```

Left subtree → `[9]`  
Right subtree → `[15,20,7]`

---

## Intuition

The algorithm builds the tree recursively.

Steps:

1. Take the first element of the preorder segment as the root.
2. Locate this root in the inorder traversal.
3. Everything left of the root in inorder belongs to the left subtree.
4. Everything right belongs to the right subtree.
5. Recursively build left and right subtrees.

To make lookup fast, we store inorder indices in a hashmap.

---

## Algorithm

1. Store the index of each element in the inorder array using a hashmap.
2. Define a recursive helper function with parameters:
   - preorder range
   - inorder range
3. Base case:
   - If range is invalid, return NULL.
4. Create root node from `preorder[preStart]`.
5. Find root index in inorder using hashmap.
6. Compute number of nodes in left subtree.
7. Recursively build:
   - Left subtree
   - Right subtree
8. Return root.

---

## Dry Run Example

Preorder:
```
[3, 9, 20, 15, 7]
```

Inorder:
```
[9, 3, 15, 20, 7]
```

Step 1:

Root = `3`

Split inorder:

```
[9] 3 [15,20,7]
```

Step 2:

Left subtree root = `9`

Right subtree root = `20`

Final Tree:

```
        3
       / \
      9  20
        /  \
       15   7
```

---

## Time and Space Complexity

Time Complexity: O(N)

Each node is processed exactly once.  
Hashmap allows O(1) lookup of inorder index.

Space Complexity: O(N)

- Hashmap storage
- Recursion stack in worst case

---

## Implementation (DFS + Recursion)

<details>
<summary><strong>C++</strong></summary>

```cpp
class Solution {
public:
    TreeNode* buildTreeHelper(vector<int>& preorder, int preStart, int preEnd,
                              vector<int>& inorder, int inStart, int inEnd,
                              unordered_map<int, int>& inMap) {
        if (preStart > preEnd || inStart > inEnd) {
            return nullptr; 
        }

        int rootVal = preorder[preStart];
        TreeNode* root = new TreeNode(rootVal);

        int inRoot = inMap[rootVal];
        int numsLeft = inRoot - inStart;

        root->left = buildTreeHelper(preorder, preStart + 1, preStart + numsLeft,
                                     inorder, inStart, inRoot - 1, inMap);

        root->right = buildTreeHelper(preorder, preStart + numsLeft + 1, preEnd,
                                      inorder, inRoot + 1, inEnd, inMap);

        return root;
    }

    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        unordered_map<int, int> inMap;

        for (int i = 0; i < inorder.size(); i++) {
            inMap[inorder[i]] = i;
        }

        return buildTreeHelper(preorder, 0, preorder.size() - 1,
                               inorder, 0, inorder.size() - 1, inMap);
    }
};
```

</details>

---

<details>
<summary><strong>Python</strong></summary>

```python
class Solution:
    def buildTree(self, preorder, inorder):

        inMap = {val: i for i, val in enumerate(inorder)}

        def helper(preStart, preEnd, inStart, inEnd):
            if preStart > preEnd or inStart > inEnd:
                return None

            rootVal = preorder[preStart]
            root = TreeNode(rootVal)

            inRoot = inMap[rootVal]
            numsLeft = inRoot - inStart

            root.left = helper(preStart + 1,
                               preStart + numsLeft,
                               inStart,
                               inRoot - 1)

            root.right = helper(preStart + numsLeft + 1,
                                preEnd,
                                inRoot + 1,
                                inEnd)

            return root

        return helper(0, len(preorder) - 1, 0, len(inorder) - 1)
```

</details>

---

<details>
<summary><strong>JavaScript</strong></summary>

```javascript
var buildTree = function(preorder, inorder) {

    const inMap = new Map();

    for (let i = 0; i < inorder.length; i++) {
        inMap.set(inorder[i], i);
    }

    function helper(preStart, preEnd, inStart, inEnd) {
        if (preStart > preEnd || inStart > inEnd) {
            return null;
        }

        const rootVal = preorder[preStart];
        const root = new TreeNode(rootVal);

        const inRoot = inMap.get(rootVal);
        const numsLeft = inRoot - inStart;

        root.left = helper(preStart + 1,
                           preStart + numsLeft,
                           inStart,
                           inRoot - 1);

        root.right = helper(preStart + numsLeft + 1,
                            preEnd,
                            inRoot + 1,
                            inEnd);

        return root;
    }

    return helper(0, preorder.length - 1, 0, inorder.length - 1);
};
```

</details>

---

## Tags

`Tree` `Binary Tree` `DFS` `Recursion` `Tree Construction` `Divide and Conquer`

---

## Variations to Practice

- Construct Binary Tree from Inorder and Postorder Traversal  
- Serialize and Deserialize Binary Tree  
- Validate Binary Search Tree  
- Binary Tree Traversals

---