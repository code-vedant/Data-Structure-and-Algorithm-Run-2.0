# Binary Search Tree Iterator

---

## Problem Links

- LeetCode: https://leetcode.com/problems/binary-search-tree-iterator/
- GeeksforGeeks: https://www.geeksforgeeks.org/implement-binary-search-treebst-iterator/

---

## Problem Description

Implement the `BSTIterator` class that represents an iterator over the inorder traversal of a binary search tree (BST).

The iterator should support the following operations:

- `BSTIterator(TreeNode* root)` initializes the iterator with the root of the BST.
- `int next()` returns the next smallest number in the BST.
- `boolean hasNext()` returns `true` if there exists a next number in the traversal.

Constraints:

- `next()` and `hasNext()` should run in **average O(1)** time.
- The iterator should use **O(H)** memory, where `H` is the height of the tree.

---

## Key Observation

Inorder traversal of a Binary Search Tree produces values in **sorted order**.

Traversal order:

```
Left → Root → Right
```

Example BST:

```
        7
       / \
      3  15
        /  \
       9   20
```

Inorder traversal:

```
3 → 7 → 9 → 15 → 20
```

---

## Intuition

Instead of generating the entire inorder traversal beforehand, we simulate the traversal **lazily** using a stack.

The stack maintains the path to the next smallest element.

Steps:

1. Push all left nodes from the root into the stack.
2. The top of the stack always represents the next smallest node.
3. When `next()` is called:
   - Pop the top node.
   - If the node has a right child, push its right subtree’s left chain.

This ensures we always maintain the correct inorder traversal state.

---

## Algorithm

Initialization:

1. Create an empty stack.
2. Push all left descendants of the root into the stack.

`next()`:

1. Pop the top node from the stack.
2. If the popped node has a right child:
   - Push all left descendants of that right child.
3. Return the node value.

`hasNext()`:

1. Return whether the stack is not empty.

---

## Dry Run

Tree:

```
        7
       / \
      3  15
        /  \
       9   20
```

Initial stack:

```
[7, 3]
```

Steps:

```
next() → 3
stack = [7]

next() → 7
push left chain of 15 → [15, 9]

next() → 9
next() → 15
next() → 20
```

Output sequence:

```
3, 7, 9, 15, 20
```

---

## Time and Space Complexity

Time Complexity:

- `next()` → O(1) amortized
- `hasNext()` → O(1)

Space Complexity:

```
O(H)
```

Where `H` is the height of the tree (stack stores path nodes).

---

## Implementation

<details>
<summary><strong>C++</strong></summary>

```cpp
class BSTIterator {
private:
    stack<TreeNode*> st;

    void pushLeft(TreeNode* node) {
        while (node) {
            st.push(node);
            node = node->left;
        }
    }

public:
    BSTIterator(TreeNode* root) {
        pushLeft(root);
    }
    
    int next() {
        TreeNode* node = st.top();
        st.pop();

        if (node->right) {
            pushLeft(node->right);
        }

        return node->val;
    }
    
    bool hasNext() {
        return !st.empty();
    }
};
```

</details>

---

<details>
<summary><strong>Python</strong></summary>

```python
class BSTIterator:

    def __init__(self, root):
        self.stack = []
        self.pushLeft(root)

    def pushLeft(self, node):
        while node:
            self.stack.append(node)
            node = node.left

    def next(self):
        node = self.stack.pop()

        if node.right:
            self.pushLeft(node.right)

        return node.val

    def hasNext(self):
        return len(self.stack) > 0
```

</details>

---

<details>
<summary><strong>JavaScript</strong></summary>

```javascript
var BSTIterator = function(root) {
    this.stack = [];
    this.pushLeft(root);
};

BSTIterator.prototype.pushLeft = function(node) {
    while (node) {
        this.stack.push(node);
        node = node.left;
    }
};

BSTIterator.prototype.next = function() {
    const node = this.stack.pop();

    if (node.right) {
        this.pushLeft(node.right);
    }

    return node.val;
};

BSTIterator.prototype.hasNext = function() {
    return this.stack.length > 0;
};
```

</details>

---

## Tags

`Tree` `Binary Tree` `Binary Search Tree` `Stack` `Iterator` `Inorder Traversal`

---

## Variations to Practice

- Kth Smallest Element in BST  
- Validate Binary Search Tree  
- Inorder Traversal  
- Convert BST to Sorted List

---