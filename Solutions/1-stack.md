# Solution to Stack Assignment

Below is the solution to the `next_greater_element` problem:

```python
class Stack:
    def __init__(self):
        self.items = []

    def push(self, item):
        self.items.append(item)

    def pop(self):
        if not self.is_empty():
            return self.items.pop()
        else:
            raise IndexError("pop from an empty stack")

    def peek(self):
        if not self.is_empty():
            return self.items[-1]
        else:
            raise IndexError("peek from an empty stack")

    def is_empty(self):
        return len(self.items) == 0


def next_greater_element(input_list):
    """
    Replace each element in the list with the next greater element to its right.
    :param input_list: List of integers
    :return: List of integers representing the next greater element to the right
    """
    # Step 1: Initialize an empty stack to keep track of indices
    stack = Stack()

    # Step 2: Initialize a result list with -1 for each element
    result = [-1] * len(input_list)

    # Step 3: Iterate through the input list from left to right
    for current_index, current_element in enumerate(input_list):
        # Step 4: While the stack is not empty and the current element is greater than the element at the top of the stack
        while not stack.is_empty() and current_element > input_list[stack.peek()]:
            # Step 4a: Update the result list at the index popped from the stack with the current element
            last_greater_index = stack.pop()
            result[last_greater_index] = current_element

        # Step 5: Push the current index onto the stack
        stack.push(current_index)

    # Step 6: Return the final result list
    return result
```