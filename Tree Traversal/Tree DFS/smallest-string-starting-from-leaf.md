# Smallest String Starting From Leaf

---

## Problem Links

- LeetCode: https://leetcode.com/problems/smallest-string-starting-from-leaf/
- GeeksforGeeks: https://www.geeksforgeeks.org/lexicographically-smallest-string-from-leaf-to-root/

---

## Problem Description

You are given the root of a binary tree where each node contains an integer value in the range `[0, 25]`.

Each value represents a lowercase letter:

```
0 -> 'a'
1 -> 'b'
...
25 -> 'z'
```

Return the **lexicographically smallest string** that starts at a **leaf node** and ends at the **root**.

Notes:

- A leaf node is a node with no children.
- The string is formed from **leaf → root**.
- If multiple strings exist, return the lexicographically smallest one.

Example rule:

```
"ab" < "aba"
```

because shorter prefix strings are considered smaller.

---

## Example

Input Tree:

```
        0
       / \
      1   2
     / \
    3   4
```

Character mapping:

```
0 -> a
1 -> b
2 -> c
3 -> d
4 -> e
```

Paths from leaf to root:

```
d -> b -> a  = "dba"
e -> b -> a  = "eba"
c -> a       = "ca"
```

Result:

```
"ca"
```

because `"ca"` is lexicographically smallest.

---

## Intuition

We need to explore **all root-to-leaf paths**.

However, the string must be constructed **from leaf to root**, so during traversal:

- Build the path from root → current node.
- When reaching a leaf, reverse the path to represent leaf → root.

Then compare the resulting string with the smallest string found so far.

DFS is ideal because it naturally explores all root-to-leaf paths.

---

## Algorithm

1. Perform DFS traversal of the tree.
2. Maintain the current path string.
3. Convert the node value into a character:

```
char = 'a' + node->val
```

4. Append the character to the current path.
5. If the node is a leaf:
   - Reverse the path to form leaf → root string.
   - Compare it with the current smallest string.
6. Recursively visit:
   - left child
   - right child
7. Return the smallest string found.

---

## Dry Run Example

Tree:

```
        0
       / \
      1   2
```

Paths:

Root → Leaf:

```
0 → 1 → "ab"
0 → 2 → "ac"
```

Leaf → Root strings:

```
"ba"
"ca"
```

Lexicographically smallest:

```
"ba"
```

---

## Time and Space Complexity

Time Complexity: O(N * H)

- N = number of nodes
- H = height of the tree
- Each path may require reversing.

Space Complexity: O(H)

- Recursion stack depth.

---

## Implementation (DFS)

<details>
<summary><strong>C++</strong></summary>

```cpp
class Solution {
public:
    string smallestFromLeaf(TreeNode* root) {
        string result = "~";
        dfs(root, "", result);
        return result;
    }

private:
    void dfs(TreeNode* node, string path, string& result) {
        if (!node) return;

        char c = 'a' + node->val;
        path = c + path;

        if (!node->left && !node->right) {
            result = min(result, path);
        }

        dfs(node->left, path, result);
        dfs(node->right, path, result);
    }
};
```

</details>

---

<details>
<summary><strong>Python</strong></summary>

```python
class Solution:
    def smallestFromLeaf(self, root):

        self.result = "~"

        def dfs(node, path):
            if not node:
                return

            char = chr(ord('a') + node.val)
            path = char + path

            if not node.left and not node.right:
                self.result = min(self.result, path)

            dfs(node.left, path)
            dfs(node.right, path)

        dfs(root, "")
        return self.result
```

</details>

---

<details>
<summary><strong>JavaScript</strong></summary>

```javascript
var smallestFromLeaf = function(root) {

    let result = "~";

    function dfs(node, path) {
        if (!node) return;

        const char = String.fromCharCode(97 + node.val);
        path = char + path;

        if (!node.left && !node.right) {
            result = result < path ? result : path;
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

`Tree` `Binary Tree` `DFS` `Backtracking` `String`

---

## Variations to Practice

- Binary Tree Paths  
- Path Sum  
- Sum Root to Leaf Numbers  
- Binary Tree Maximum Path Sum

---