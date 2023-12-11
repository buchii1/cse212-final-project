# Tree

## 1.1 Overview

Trees are a fundamental data structure in computer science that have widespread applications in various fields. They are hierarchical structures composed of **nodes** connected by **edges**. In this tutorial, we will explore the basics of trees, their types, and demonstrate their implementation in Python.

## 1.2 Basic Tree Structure

At the top of the hierarchy is the **root node**, and the nodes that have no children are called **leaves**. Nodes in a tree are connected in a way that there is exactly one path between any two nodes.

#### Nodes

Each node in a tree contains a **value or data** and may have a reference to its **children nodes**. Nodes with the same parent are considered **siblings**. The **depth** of a node is the length of the path from the root to that node. The **height** of a tree is the length of the longest path from the root to a leaf.

#### Edges

Edges in a tree represent the relationships between nodes. Each node (except the root) has exactly one **parent node**, and zero or more **child nodes**. The edges are directed, meaning they have a specific direction - going from parent to child.

#### Nodes in Python

Let's represent the basic tree structure in Python:

```python
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.children = []
```

This code defines a simple class named `TreeNode`.  Each node has a `value` and a list of `children`, which starts with an empty list.

```python
# Creating nodes
root = TreeNode('A')
node_b = TreeNode('B')
node_c = TreeNode('C')
node_d = TreeNode('D')
node_e = TreeNode('E')
```

Here, five instances of the `TreeNode` class are created, representing nodes in a tree. At this point, the children attribute of each node is an empty list.

```python
# Connecting nodes
root.children = [node_b, node_c]
node_b.children = [node_d, node_e]
```

This part establishes the connections between the nodes, forming a simple tree structure. The `root` node, with the value 'A', has two children: the node with value 'B' and the node with value 'C'. Similarly, the 'B' node has two children: 'D' and 'E'. This creates a tree with 'A' as the root and 'B' and 'C' as its immediate children, and 'D' and 'E' as children of 'B'.


The resulting tree can be visually represented as follows:

```markdown
    A
   / \
  B   C
 / \
D   E
```

## 1.3 Types of Trees

#### Binary Trees

A **binary tree** is a hierarchical data structure in which each node has at most two children, referred to as the left child and the right child. The structure is recursive, meaning that each child of a node is the root of its subtree, itself a binary tree.

#### Binary Tree Example

Consider the following binary tree:

```markdown
        5
       / \
      3   8
     / \ / \
    1  4 7  9
```

Here, 5 is the root, and each node has at most two children. The left subtree of the root (3 and its descendants) is a binary tree, and the right subtree (8 and its descendants) is also a binary tree.

#### Types of Binary Trees

**Full Binary Tree:** A binary tree in which every node has either 0 or 2 children.

```markdown
        5
       / \
      3   8
     / \
    1   4
```

**Complete Binary Tree:** A binary tree in which all levels are completely filled, except possibly the last level, which is filled from left to right.

```markdown
        5
       / \
      3   8
     / \ 
    1   4
```

**Perfect Binary Tree:** A binary tree in which all internal nodes have exactly two children, and all leaf nodes are at the same level.

```markdown
        5
       / \
      3   8
     / \ / \
    1  4 7  9
```

#### Binary Tree Operations

##### Traversal
Traversal involves visiting each node in a specific order. Three common types are:

- **In-order:** Left, Root, Right
- **Pre-order:** Root, Left, Right
- **Post-order:** Left, Right, Root

```python
class BinaryTreeNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

def in_order_traversal(node):
    if node:
        in_order_traversal(node.left)
        print(node.value, end=" ")
        in_order_traversal(node.right)

# Creating a binary tree
tree = BinaryTreeNode(5)
tree.left = BinaryTreeNode(3)
tree.right = BinaryTreeNode(8)
tree.left.left = BinaryTreeNode(1)
tree.left.right = BinaryTreeNode(4)
tree.right.left = BinaryTreeNode(7)
tree.right.right = BinaryTreeNode(9)

# Performing in-order traversal
in_order_traversal(tree)
# Output: 1 3 4 5 7 8 9
```

##### Search
Finding a specific node in the tree. In a well-balanced tree, the time complexity is **O(log n)**.

```python
def search_bst(root, target):
    if not root or root.value == target:
        return root
    if target < root.value:
        return search_bst(root.left, target)
    else:
        return search_bst(root.right, target)
```

##### Insertion and Deletion
Adding or removing nodes while maintaining the binary tree properties.

##### Performance in Terms of Big O
In a well-balanced binary tree, (e.g., AVL tree), the average time complexities are as follows:

- **Search Operation:** O(log n)
- **Insertion Operation:** O(log n)
- **Deletion Operation:** O(log n)

These complexities depend on the height of the tree, and a well-balanced tree ensures logarithmic height. However, in the worst case (unbalanced tree), the complexity can degrade to O(n), resembling a linked list.

#### Binary Search Trees (BST)

A BST is a hierarchical data structure that follows the principles of a binary tree with an additional constraint: the key values of nodes in the left subtree of any node are less than the key value of the node, and the key values of nodes in the right subtree are greater than the key value of the node.

##### Binary Search Tree Example
Consider the following Binary Search Tree: 

```markdown
        8
       / \
      3   10
     / \    \
    1   6    14
       / \   /
      4   7  13
```

##### Key Properties
1. **Binary Tree Structure:** Each node in a BST has at most two children: a left child and a right child.
2. **Ordering Constraint:** For any node in the tree, all nodes in its left subtree have key values less than the node's key, and all nodes in its right subtree have key values greater than the node's key.

##### Operations
1. **Search Operation:** Searching for a specific key involves traversing the tree starting from the root. At each step, the search narrows down based on whether the key is less than, equal to, or greater than the current node's key.
2. **Insertion Operation:** To insert a new key, the tree is traversed similarly to the search operation. When a suitable empty position is found (i.e., a leaf), the new node is added with the appropriate relationship to its parent.
3. **Deletion Operation:** Deleting a node from the BST involves three cases:
    - If the node has no children, it is simply removed.
    - If the node has one child, the node is replaced by its child.
    - If the node has two children, it is replaced by its in-order successor (or predecessor), and the successor's original position is then dealt with.

##### Example of a Binary Search Tree in Python

```python
class TreeNode:
    def __init__(self, key):
        # Constructor for the TreeNode class
        self.key = key  # The key value stored in the node
        self.left = None  # Reference to the left child
        self.right = None  # Reference to the right child

def insert(root, key):
    # Recursive function to insert a key into the BST
    if not root:
        # If the root is None, create a new node with the given key
        return TreeNode(key)
    if key < root.key:
        # If the key is less than the current node's key, insert into the left subtree
        root.left = insert(root.left, key)
    elif key > root.key:
        # If the key is greater than the current node's key, insert into the right subtree
        root.right = insert(root.right, key)
    return root

def search(root, key):
    # Recursive function to search for a key in the BST
    if not root or root.key == key:
        # If the root is None or the key is found, return the root
        return root
    if key < root.key:
        # If the key is less than the current node's key, search in the left subtree
        return search(root.left, key)
    return search(root.right, key)

def minValueNode(node):
    # Helper function to find the node with the minimum key in a subtree
    current = node
    while current.left:
        current = current.left
    return current

def deleteNode(root, key):
    # Recursive function to delete a node with a given key from the BST
    if not root:
        return root
    if key < root.key:
        # If the key is less than the current node's key, delete from the left subtree
        root.left = deleteNode(root.left, key)
    elif key > root.key:
        # If the key is greater than the current node's key, delete from the right subtree
        root.right = deleteNode(root.right, key)
    else:
        # If the key is found, perform deletion
        if not root.left:
            return root.right
        elif not root.right:
            return root.left
        root.key = minValueNode(root.right).key
        root.right = deleteNode(root.right, root.key)
    return root

def inorderTraversal(root):
    # Helper function for in-order traversal of the BST
    result = []
    if root:
        result += inorderTraversal(root.left)
        result.append(root.key)
        result += inorderTraversal(root.right)
    return result

# Example Usage
root = None
keys = [8, 3, 10, 1, 6, 14, 4, 7, 13]

# Insert keys into the BST
for key in keys:
    root = insert(root, key)

# In-order Traversal (prints sorted elements)
print("In-order Traversal:", inorderTraversal(root)) # -> [1, 3, 4, 6, 7, 8, 10, 13, 14]

# Search for key 6
search_result = search(root, 6)
print("Search Result:", search_result.key if search_result else "Not Found") # -> 6

# Delete node with key 10
root = deleteNode(root, 10)
print("After Deletion (key 10):", inorderTraversal(root)) # -> [1, 3, 4, 6, 7, 8, 13, 14]
```

This code includes the following operations:

1. **Insertion:** Adds elements to the BST.
2. **Search:** Searches for a specific key in the BST.
3. **Deletion:** Deletes a node with a specific key from the BST.
4. **In-order Traversal:** Prints the elements of the BST in sorted order.

You can run this code to observe the behavior of these operations in a Binary Search Tree.


#### AVL Trees

An AVL tree is a self-balancing binary search tree (BST) where the balance factor of every node is within the range of -1, 0, or 1. The balance factor is defined as the difference in height between the left and right subtrees of a node. AVL trees maintain their balance during insertion and deletion operations, ensuring that the height of the tree remains logarithmic.

##### Maintaining Balance

In an AVL tree, every time a node is inserted or deleted, the tree is checked for balance. If the balance factor of any node violates the -1, 0, 1 rule, rotations are performed to restore balance.

##### Rotations

**Left Rotation:** Used to balance a right-heavy subtree.

```markdown
     A                 B
      \               / \
       B      ->     A   C
        \
         C
```

**Right Rotation:** Used to balance a left-heavy subtree.

```markdown
       C             B
      /             / \
     B       ->    A   C
    /
   A
```

**Left-Right Rotation (Double Rotation):** Used to balance a left-heavy subtree with a left-heavy child. It involves a left rotation followed by a right rotation.

```markdown
     A             C
      \           / \
       C    ->   A   E
      / \
     D   E
```

**Right-Left Rotation (Double Rotation):** Used to balance a right-heavy subtree with a right-heavy child. It involves a right rotation followed by a left rotation.

```markdown
       E         C
      /         / \
     C    ->   A   E
      / \
     A   D
```

#### Performance

The balancing property of AVL trees ensures that the height of the tree remains logarithmic, leading to efficient search, insertion, and deletion operations. In a well-maintained AVL tree, the time complexities are O(log n) for these operations.

#### Example of an AVL Tree in Python

```python
class AVLTreeNode:
    def __init__(self, value):
        # Constructor for AVL tree node
        self.value = value  # The value of the node
        self.height = 1  # Height of the node (initially set to 1)
        self.left = None  # Reference to the left child
        self.right = None  # Reference to the right child

def height(node):
    # Helper function to get the height of a node
    if not node:
        return 0
    return node.height

def balance_factor(node):
    # Helper function to calculate the balance factor of a node
    if not node:
        return 0
    return height(node.left) - height(node.right)

def update_height(node):
    # Helper function to update the height of a node based on its children's heights
    if not node:
        return 0
    node.height = 1 + max(height(node.left), height(node.right))
    return node.height

def left_rotate(y):
    # Perform a left rotation on the given nodes
    x = y.right
    T2 = x.left

    # Rotation steps
    x.left = y
    y.right = T2

    # Update heights after rotation
    update_height(y)
    update_height(x)

    return x

def right_rotate(x):
    # Perform a right rotation on the given nodes
    y = x.left
    T2 = y.right

    # Rotation steps
    y.right = x
    x.left = T2

    # Update heights after rotation
    update_height(x)
    update_height(y)

    return y

def balance(node):
    # Helper function to get the balance factor of a node
    if not node:
        return 0
    return height(node.left) - height(node.right)

def insert(root, key):
    # Recursive function to insert a key into the AVL tree while maintaining balance
    if not root:
        # If the root is None, create a new node with the given key
        return AVLTreeNode(key)

    # Perform standard BST insertion
    if key < root.value:
        root.left = insert(root.left, key)
    else:
        root.right = insert(root.right, key)

    # Update height of the current node
    update_height(root)

    # Get the balance factor of this ancestor node
    balance_factor_root = balance(root)

    # Left Heavy
    if balance_factor_root > 1:
        # Left-Left
        if key < root.left.value:
            return right_rotate(root)
        # Left-Right
        else:
            root.left = left_rotate(root.left)
            return right_rotate(root)

    # Right Heavy
    if balance_factor_root < -1:
        # Right-Right
        if key > root.right.value:
            return left_rotate(root)
        # Right-Left
        else:
            root.right = right_rotate(root.right)
            return left_rotate(root)

    return root

def print_tree(root, level=0, prefix="Root: "):
    # Helper function to print the AVL tree structure with balance factors
    if root:
        print(" " * (level * 4) + prefix + str(root.value) + " (BF: " + str(balance(root)) + ")")
        if root.left or root.right:
            print_tree(root.left, level + 1, "L--- ")
            print_tree(root.right, level + 1, "R--- ")

# Example Usage
avl_tree = None
values_to_insert = [10, 5, 15, 2, 7, 12, 17]

# Insert values into the AVL tree
for value in values_to_insert:
    avl_tree = insert(avl_tree, value)

# Print the AVL tree
print_tree(avl_tree)
```

This Python example includes a basic AVL tree implementation with insertion and rotations. The insert function inserts a key into the AVL tree while maintaining balance. The print_tree function helps visualize the tree structure.

Feel free to run this code and observe how the AVL tree stays balanced after each insertion. The rotations (left, right, left-right, right-left) are performed as needed to maintain the balance factor of each node within the range of -1, 0, or 1.

## 1.4 Usages


Trees are versatile data structures and find applications in various domains due to their hierarchical and organized nature. Here are some common use cases for trees:

1. **File Systems:** File systems on computers are often organized as tree structures. Directories (folders) can contain files or other directories, creating a hierarchical organization.
2. **Organization Charts:** Representing the hierarchy of employees within an organization. Each node in the tree represents an employee, and the edges represent the reporting relationships.
3. **HTML Document Object Model (DOM):** BSTs are used in search operations where the elements in the tree are ordered. They provide efficient searching, insertion, and deletion operations.
4. **Network Routing Tables:** Representing the routing information in computer networks. Each node corresponds to a network address, and the tree structure helps efficiently route data to its destination.
5. **Family Trees and Genealogy:** Representing family relationships and ancestry. Each node can represent an individual, and edges represent parent-child relationships.

## 1.4 Problem Solving with Trees

**Problem 1:** Write a function `is_valid_inorder(tree)` that takes a binary tree as input and checks if the elements in the tree, when traversed in in-oder, form a valid sequence in ascending order.

**Solution:**

```python
class TreeNode:
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

def is_valid_inorder(root):
    """
    Check if the elements in the binary tree form a valid sequence when traversed in in-order.
    Args:
    - root (TreeNode): The root of the binary tree.
    Returns:
    - bool: True if the in-order traversal is valid, False otherwise.
    """
    def validate_inorder(node, lower=float('-inf'), upper=float('inf')):
        if not node:
            return True

        # Check the current node's value
        if not lower < node.key < upper:
            return False

        # Traverse the left subtree with updated upper limit
        if not validate_inorder(node.left, lower, node.key):
            return False

        # Traverse the right subtree with updated lower limit
        if not validate_inorder(node.right, node.key, upper):
            return False

        return True

    return validate_inorder(root)
```

**Test Cases:**

```python
# Test Case 1: Valid Binary Search Tree
bst_root_valid = TreeNode(2)
bst_root_valid.left = TreeNode(1)
bst_root_valid.right = TreeNode(3)

assert is_valid_inorder(bst_root_valid) == True

# Test Case 2: Invalid Binary Search Tree (Duplicate Value)
bst_root_invalid_duplicate = TreeNode(2)
bst_root_invalid_duplicate.left = TreeNode(2)
bst_root_invalid_duplicate.right = TreeNode(3)

assert is_valid_inorder(bst_root_invalid_duplicate) == False

# Test Case 3: Invalid Binary Search Tree (Out of Order)
bst_root_invalid_order = TreeNode(2)
bst_root_invalid_order.left = TreeNode(3)
bst_root_invalid_order.right = TreeNode(1)

assert is_valid_inorder(bst_root_invalid_order) == False

# Test Case 4: Empty Tree
assert is_valid_inorder(None) == True

# Test Case 5: Valid Binary Search Tree (Complex)
bst_root_complex_valid = TreeNode(10)
bst_root_complex_valid.left = TreeNode(5)
bst_root_complex_valid.right = TreeNode(15)
bst_root_complex_valid.left.left = TreeNode(3)
bst_root_complex_valid.left.right = TreeNode(7)
bst_root_complex_valid.right.right = TreeNode(20)

assert is_valid_inorder(bst_root_complex_valid) == True

print("All test cases passed!")
```

**Problem 2:** You are given the root of a binary tree. Write a function `is_balanced` to determine if the tree is balanced.

A binary tree is considered balanced if the height of the two subtrees of every node never differs by more than one.

**Solution:**

```python
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

def is_balanced(root: TreeNode) -> bool:
    """
    Check if the given binary tree is balanced.
    Args:
    - root (TreeNode): The root of the binary tree.
    Returns:
    - bool: True if the tree is balanced, False otherwise.
    """

    def height(node):
        """
        Helper function to calculate the height of a node.
        Args:
        - node (TreeNode): The node.
        Returns:
        - int: The height of the node.
        """
        if not node:
            return 0
        left_height = height(node.left)
        right_height = height(node.right)
        return max(left_height, right_height) + 1

    def is_balanced_helper(node):
        """
        Helper function to check if the subtree rooted at the given node is balanced.
        Args:
        - node (TreeNode): The root of the subtree.
        Returns:
        - bool: True if the subtree is balanced, False otherwise.
        """
        if not node:
            return True

        left_height = height(node.left)
        right_height = height(node.right)

        if abs(left_height - right_height) > 1:
            return False

        return is_balanced_helper(node.left) and is_balanced_helper(node.right)

    return is_balanced_helper(root)
```

**Test Cases:**

```python
# Test Case 1: Balanced Tree
# Tree structure:
#        1
#       / \
#      2   3
#     / \
#    4   5
balanced_tree = TreeNode(1)
balanced_tree.left = TreeNode(2)
balanced_tree.right = TreeNode(3)
balanced_tree.left.left = TreeNode(4)
balanced_tree.left.right = TreeNode(5)

assert is_balanced(balanced_tree) == True

# Test Case 2: Unbalanced Tree
# Tree structure:
#        1
#       /
#      2
#     /
#    3
unbalanced_tree = TreeNode(1)
unbalanced_tree.left = TreeNode(2)
unbalanced_tree.left.left = TreeNode(3)

assert is_balanced(unbalanced_tree) == False

# Test Case 3: Empty Tree
assert is_balanced(None) == True

# Test Case 4: Single Node Tree
single_node_tree = TreeNode(1)
assert is_balanced(single_node_tree) == True

print("All test cases passed!")
```

## 1.5 Assignment

**Problem:** Given a binary tree, find the maximum path sum. The path may start and end at any node in the tree.

A path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain at least one node and does not need to go through the root.

*Use the boilerplate below:*

```python
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

def max_path_sum(root: TreeNode):
    """
    Find the maximum path sum in a binary tree.
    Args:
    - root (TreeNode): The root of the binary tree.
    Returns:
    - int: The maximum path sum.
    """
    # TODO: Implement the solution here
    pass
```

**Test Cases:**

```python
# Test Case 1: Tree with Positive and Negative Values
# Tree structure:
#        10
#       /  \
#      2    10
#     / \     \
#    20  1    -25
#            / \
#           3   4
tree1 = TreeNode(10)
tree1.left = TreeNode(2)
tree1.right = TreeNode(10)
tree1.left.left = TreeNode(20)
tree1.left.right = TreeNode(1)
tree1.right.right = TreeNode(-25)
tree1.right.right.left = TreeNode(3)
tree1.right.right.right = TreeNode(4)

assert max_path_sum(tree1) == 42

# Test Case 2: Tree with Single Node
single_node_tree = TreeNode(5)
assert max_path_sum(single_node_tree) == 5

# Test Case 3: Tree with Negative Values
# Tree structure:
#       -10
#       /  \
#     -20  -30
negative_tree = TreeNode(-10)
negative_tree.left = TreeNode(-20)
negative_tree.right = TreeNode(-30)

assert max_path_sum(negative_tree) == -10

# Test Case 4: Tree with All Negative Values
# Tree structure:
#       -5
#       / \
#     -10 -20
#     /    /
#   -15  -30
all_negative_tree = TreeNode(-5)
all_negative_tree.left = TreeNode(-10)
all_negative_tree.right = TreeNode(-20)
all_negative_tree.left.left = TreeNode(-15)
all_negative_tree.right.left = TreeNode(-30)

assert max_path_sum(all_negative_tree) == -5

print("All test cases passed!")
```