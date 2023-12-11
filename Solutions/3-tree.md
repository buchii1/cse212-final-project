# Solution to Tree Assignment

Below is the solution to the **Binary Tree Maximum Path Sum** problem:

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

    # Helper function to calculate the maximum path sum for each node
    def max_path_sum_helper(node, max_sum):
        # Base case: if the node is None, the maximum path sum is 0
        if not node:
            return 0

        # Calculate the maximum path sum for the left and right subtrees
        left_sum = max(0, max_path_sum_helper(node.left, max_sum))
        right_sum = max(0, max_path_sum_helper(node.right, max_sum))

        # Update the maximum path sum considering the current node
        max_sum[0] = max(max_sum[0], left_sum + right_sum + node.value)

        # Return the maximum path sum considering only one subtree (left or right)
        return max(left_sum, right_sum) + node.value

    # Initialize the maximum path sum to the smallest possible integer value
    max_sum = [float('-inf')]

    # Start the recursive calculation from the root
    max_path_sum_helper(root, max_sum)

    return max_sum[0]
```