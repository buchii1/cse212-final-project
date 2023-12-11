# Stack

## 1.1 Overview

A stack is a fundamental data structure that organizes elements in a linear order following the Last In, First Out (LIFO) principle. In a stack, elements are added and removed from the top, which is the end of the structure. It can be envisioned as a collection of items stacked on top of each other, much like a stack of plates.

## 1.2 Basic Operations

A stack supports several basic operations that make it versatile and efficient data structure We will use a basic example of a list-based stack in explaining the operations.

```python
class Stack:
    # List-based stack implementation.
    def __init__(self):
        self.items = []
    ...
```

The basic operations are as follows:

### i. Push Operation

The push operation involves adding an element to the top of the stack. Stacks can dynamically grow as elements are pushed onto them. The size of the stack is not fixed, and it can accommodate an arbitrary number of elements.

```python
# A method of the Stack class.
def push(self, item):
    self.items.append(item)
```

The `push` method uses the `append ` method of the list to add a specified element to the end of the stack. 

```shell
Before Push          After Push
+---+                +---+
| 3 |                | 3 |
+---+                +---+
| 5 |                | 5 |
+---+                +---+
| 8 |                | 8 |
+---+    push(2)     +---+
        -------->    | 2 |
                     +---+
```

### ii. Pop Operation
The pop operation involves removing the top element from the stack.

```python
# A method of the Stack class.
def pop(self):
    if not self.is_empty():
        return self.items.pop()
    else:
        raise IndexError("pop from an empty stack")
```

The `pop` method checks if the stack is not empty. If the stack is not empty, it uses the `pop` method of the list to remove and return the last element. If the stack is empty, it raises an `IndexError` with a message indicating an attempt to pop from an empty stack.


```shell
Before Pop           After Pop
+---+                +---+
| 3 |                | 3 |
+---+                +---+
| 5 |                | 5 |
+---+                +---+
| 8 |                | 8 |
+---+    pop()       +---+
| 2 |   -------->    |   |
+---+                +---+
```

### iii. Peek/Top Operation

The peek operation retrieves the top element without removing it.

```python
# A method of the Stack class.
def peek(self):
    if not self.is_empty():
        return self.items[-1]
    else:
        raise IndexError("peek from an empty stack")
```

Here, the `peek` method checks if the stack is not empty. If the stack is not empty, it returns the last element of the stack(`self.items[-1]`). If the stack is empty, it raises an `IndexError` with a message indicating that peek was attempted on an empty stack.

### iv. isEmpty Operation

The isEmpty operation checks if the stack is empty.

```python
# A method of the Stack class.
def is_empty(self):
    return len(self.items) == 0
```

The `isEmpty` method checks if the length of the list representing the stack is equal to 0. If the length is 0, the method returns `True`, indicating that the stack is empty. If the length is greater than 0, the method returns `False`, indicating that the stack contains elements.

```shell
+---+
|   |   isEmpty()
+---+   -------->
|   |   Result: True
+---+
|   |
+---+
|   |
+---+
```

## 1.3 Usages

Stacks find application in various scenarios due to their Last In, First Out (LIFO) nature. Here are some common uses cases and usages of stacks:

- **Function Call Management:** Stacks are used to manage function calls in programming languages. When a function is called, its context (local variables, return address, etc.) is pushed onto the call stack. When the function execution is complete, its context is popped off the stack. 
- **Undo Mechanism:** Many applications utilize stacks to implement undo functionality. Each action performed is pushed onto a stack, and the undo operation involves popping the last action off the stack to revert the state.
- **Browser History:** The backward and forward navigation in web browsers is often implemented using two stacks. When a new page is visited, the current page is pushed onto the back stack. Pressing the back button pops the top page off the back stack and pushes it onto the forward stack.

## 1.4 Performance Analysis

Let's delve into the Big O performance of each fundamental operation in a stack that we have analyzed.

Operation | Big O | 
--------- | ----- | 
Push | O(1) | 
Pop | O(1) | 
Peek | O(1)
isEmpty | O(1)

## 1.5 Problem Solving with Stack

**Problem:** Check if a given string containing parenthesis is well-formed / properly nested and closed.

**Solution:**

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


def is_well_formed(expression):
    """
    Check if the given string with parentheses is well-formed.
    :param expression: String with parentheses
    :return: True if well-formed, False otherwise
    """
    stack = Stack()
    parentheses = {'(': ')', '[': ']', '{': '}'}

    for char in expression:
        if char in parentheses.keys():
            # Opening parentheses, push onto the stack
            stack.push(char)
        elif char in parentheses.values():
            # Closing parentheses, check if matching pair exists
            if stack.is_empty() or parentheses[stack.pop()] != char:
                return False

    # The string is well-formed if the stack is empty at the end
    return stack.is_empty()


# Example Usage
expression1 = "{[()]}"  # Well-formed
expression2 = "{[(])}"  # Not well-formed

print(f"Is '{expression1}' well-formed? {is_well_formed(expression1)}")  # Output: True
print(f"Is '{expression2}' well-formed? {is_well_formed(expression2)}")  # Output: False
```

The `is_well_formed` function uses a stack to keep track of opening parentheses. When an opening parentheses is encountered, it's pushed onto the stack. When a closing parentheses is encountered, it checks if there's a matching opening parentheses at the top of the stack. If the parentheses are well-formed, the stack should be empty at the end.

## 1.6 Assignment

**Problem:** Write a function that takes a list of integers and returns a new list where each element is replaced with the next greater element to it's right. If there is no greater element, replace it with -1.

Make use of the boilerplate below:

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
    # TODO: Implement the logic for the next_greater_element function
    pass
```

**Test Cases:**

```python
# Test Case 1: Basic Input
input_list_1 = [4, 2, 8, 6, 5]
# The next greater elements are [8, 8, -1, -1, -1]
expected_output_1 = [8, 8, -1, -1, -1]

# Test Case 2: All Elements in Descending Order
input_list_2 = [5, 4, 3, 2, 1]
# There is no next greater element for any element, so the output should be [-1, -1, -1, -1, -1]
expected_output_2 = [-1, -1, -1, -1, -1]

# Test Case 3: All Elements in Ascending Order
input_list_3 = [1, 2, 3, 4, 5]
# The next greater elements are [2, 3, 4, 5, -1]
expected_output_3 = [2, 3, 4, 5, -1]

# Test Case 4: Random Input
input_list_4 = [3, 1, 7, 4, 2, 8]
# The next greater elements are [7, 7, 8, 8, 8, -1]
expected_output_4 = [7, 7, 8, 8, 8, -1]

# Test Case 5: Empty Input
input_list_5 = []
# There are no elements in the input, so the output should be an empty list []
expected_output_5 = []

# Test Case 6: Single Element
input_list_6 = [9]
# There is no next greater element for the single element, so the output should be [-1]
expected_output_6 = [-1]

# Test Case 7: Duplicate Elements
input_list_7 = [3, 3, 1, 1, 4, 4]
# The next greater elements are [4, 4, 4, 4, -1, -1]
expected_output_7 = [4, 4, 4, 4, -1, -1]

# Test Case 8: Large Input
input_list_8 = list(range(10**6, 0, -1))
# All elements are in descending order, so the output should be a list of -1s of the same length
expected_output_8 = [-1] * 10**6

# Running the tests
assert next_greater_element(input_list_1) == expected_output_1
assert next_greater_element(input_list_2) == expected_output_2
assert next_greater_element(input_list_3) == expected_output_3
assert next_greater_element(input_list_4) == expected_output_4
assert next_greater_element(input_list_5) == expected_output_5
assert next_greater_element(input_list_6) == expected_output_6
assert next_greater_element(input_list_7) == expected_output_7
assert next_greater_element(input_list_8) == expected_output_8

print("All test cases passed!")
```