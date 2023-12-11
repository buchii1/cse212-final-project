# Set

## 1.1 Overview

A set is a collection of distinct and unordered elements. Each element in a set is unique, and the order of elements does not matter. In Python, the `set` datatype is used to represent sets.

##### Notation
Sets are often denoted using curly braces `{}`, and elements are listed inside the braces, separated by commas. For example: `A = {1,2,3,4}`

##### Elements
- **Distinct:** Each element in a set is unique. Duplicates are not allowed.
- **Unordered:** The order of elements in a set has no significance.

## 1.2 Set Operations

### i. Adding Elements

Adding an element to a set involves placing a new, unique element into the set.

```python
my_set.add(value)
```

The `add` method is used to insert a single element into the set. The element is placed at an arbitrary position within the set, as sets are unordered. If the element is already present in the set, the `add()` operation has no effect.

```markdown
Original Set: {1, 2, 3}
After Adding 4: {1, 2, 3, 4}
```

The time complexity for adding an element to a set is **O(1)**; which is constant time.

### ii.Removing Elements

Removing an element from a set involves eliminating a specific element from the set.

```python
my_set.remove(value)
```

The `remove` method deletes the specified element from the set. If the element is not present, a `KeyError` is raised. To avoid this, you can use conditional rendering or the `discard` method, which removes the element if present and does nothing otherwise.

```python
my_set.discard(value)
```

```markdown
Original Set: {1, 2, 3, 4}
After Removing 3: {1, 2, 4}
```

The time complexity for removing an element to a set is **O(1)**; which is constant time.

### iii. Checking Membership

Checking membership involves determining whether a specific element is present in the set.

```python
is_present = value in my_set
```

The `in` operator is used to check whether a specific element is present in the set. If the element is present, the result is `True`; If the element is not present, the result is `False`.

```markdown
Set: {1, 2, 3, 4}
Is 3 Present? True
Is 5 Present? False
```

The time complexity for checking for membership in a set is **O(1)**; which is constant time.

### iv. Union

The union of two sets, denoted `A ∪ B`, is a new set containing all unique elements from both sides.

`A ∪ B = {x ∣ x ∈ A or x ∈ B}`

```python
set_union = set1.union(set2)
```

The `union()` method combines elements from two sets, creating a new set that contains all unique elements from both sets. The original set remain unchanged.

```markdown
  A         B         A ∪ B
1 2 3     3 4 5     1 2 3 4 5
```

The time complexity is determined by that of the smaller set.

### v. Intersection

The intersection of two sets, denoted `A ∩ B`, is a new set containing elements common to both sets.

`A ∩ B = {x ∣ x ∈ A and x ∈ B}`

```python
intersection_result = set_c.intersection(set_d)
```

The `intersection()` method returns a new set containing elements that are common to both sets. The original sets remain unchanged.

```markdown
  A        B         A ∩ B
1 2 3    3 4 5         3
```

The time complexity is determined by the size of the smaller set.

### vi. Difference

The difference of two sets, denoted `A − B`, is a new set containing elements from the first set that are not in the second set.

`A − B = {x ∣ x ∈ A and x ∈/ B}`

```python
difference_result = set_e.difference(set_f)
```

The `difference()` method returns a new set containing elements that are unique to the first set and not present in the second set. The original sets remain unchanged.

```python
  A        B         A - B
1 2 3    3 4 5        1 2
```

The time complexity is determined by thr size of the first set.

## 1.3 Usages

Sets are versatile data structures that find applications in various domains due to their unique properties. Here are some of the usages:

1. **Removing Duplicates:** Sets are particularly effective for eliminating duplicate elements from a collection, ensuring that each element is unique.
2. **Membership Testing:** Sets provide efficient membership testing operations, allowing quick checks to determine whether a specific element is part of the set.
3. **Graphical Theory:** Sets are used in graph theory to represent vertices, edges, and various subsets of a graph, simplifying graph-related computations.
4. **Cryptography:** Sets can represent sets of valid keys, possible encryption algorithms, or other cryptographic elements.
5. **Statistical Analysis:** Sets can represent distinct categories or groups, facilitating the analysis of data with respect to different criteria.

## 1.4 Problem Solving with Set

**Problem 1:** You are managing student enrollments for various courses in a university. Each student is associated with a set of courses they are enrolled in. Your task is to create a system that supports various operations involving these sets.

Implement a class `EnrollmentSystem` with the following functionalities:

1. **Enroll Students:** Add a new student and their set of enrolled courses to the system.
2. **Drop Courses:** Remove specific courses from a student's enrollment.
3. **Common Courses:** Find the common courses enrolled by a given pair of students.
4. **Union of Courses:** Find the union of courses enrolled by a given pair of students.
5. **Students in a Course:** Find the set of students enrolled in a specific course.

**Solution:**

```python
class EnrollmentSystem:
    def __init__(self):
        # Initialize an empty dictionary to store student enrollments
        self.enrollments = {}

    def enroll_student(self, student_id, courses):
        """
        Enroll a student in a set of courses.
        """
        # If the student already exists, update their enrolled courses
        if student_id in self.enrollments:
            self.enrollments[student_id].update(courses)
        else:
            # If the student is new, create a new set of enrolled courses
            self.enrollments[student_id] = set(courses)

    def drop_courses(self, student_id, courses_to_drop):
        """
        Drop specific courses from a student's enrollment.
        """
        # If the student exists, remove the specified courses
        if student_id in self.enrollments:
            self.enrollments[student_id] -= courses_to_drop

    def common_courses(self, student1_id, student2_id):
        """
        Find the common courses between two students.
        """
        # If both students exist, calculate the intersection of their enrolled courses
        if student1_id in self.enrollments and student2_id in self.enrollments:
            common_courses = self.enrollments[student1_id] & self.enrollments[student2_id]
            return common_courses
        else:
            # If one or both students do not exist, return an empty set
            return set()

    def union_of_courses(self, student1_id, student2_id):
        """
        Find the union of courses between two students.
        """
        # If both students exist, calculate the union of their enrolled courses
        if student1_id in self.enrollments and student2_id in self.enrollments:
            union_courses = self.enrollments[student1_id] | self.enrollments[student2_id]
            return union_courses
        else:
            # If one or both students do not exist, return an empty set
            return set()

    def students_in_course(self, course):
        """
        Find the set of students enrolled in a specific course.
        """
        # Use a set comprehension to collect students who are enrolled in the specified course
        students_in_course = {student_id for student_id, courses in self.enrollments.items() if course in courses}
        return students_in_course
```

**Test Cases:**

```python
def run_tests():
    # Test Case 1: Enroll students, drop courses, and find common courses
    enrollment_system = EnrollmentSystem()

    enrollment_system.enroll_student("A123", {"Math", "Physics", "Chemistry"})
    enrollment_system.enroll_student("B456", {"Physics", "Biology", "History"})
    enrollment_system.enroll_student("C789", {"Math", "Computer Science", "History"})

    enrollment_system.drop_courses("A123", {"Chemistry"})
    enrollment_system.drop_courses("B456", {"History"})

    common_courses_result = enrollment_system.common_courses("A123", "B456")
    assert common_courses_result == {'Physics'}

    # Test Case 2: Enroll students, find union of courses, and find students in a course
    enrollment_system = EnrollmentSystem()

    enrollment_system.enroll_student("X111", {"Math", "Physics", "Chemistry"})
    enrollment_system.enroll_student("Y222", {"Physics", "Biology", "History"})
    enrollment_system.enroll_student("Z333", {"Math", "Computer Science", "History"})

    union_result = enrollment_system.union_of_courses("X111", "Y222")
    assert union_result == {'Math', 'Physics', 'Chemistry', 'Biology', 'History'}

    students_in_course_result = enrollment_system.students_in_course("Physics")
    assert students_in_course_result == {'X111', 'Y222'}

    # Test Case 3: Enroll a new student, drop courses, and find common courses (non-existing student)
    enrollment_system = EnrollmentSystem()

    enrollment_system.enroll_student("P999", {"English", "Art", "History"})
    
    # Dropping courses for a non-existing student should not raise an error
    enrollment_system.drop_courses("Q888", {"Art"})

    # Finding common courses with a non-existing student should return an empty set
    common_courses_result = enrollment_system.common_courses("P999", "Q888")
    assert common_courses_result == set()

    print("All tests passed!")

# Run the corrected test cases
run_tests()
```


## 1.5 Assignment

**Problem:** You are given a set of integers, and your task is to create a function that determines if it can be partitioned into two subsets with equal sums. 

**Explanation:** 

- The `can_partition_into_equal_sum` function takes a list of integers as input.
- It should return `True` if the set of integers can be partitioned into two subsets with equal sums; otherwise, it should return `False`.

*Use the boilerplate below:*

```python
def can_partition_into_equal_sum(nums):
    # Your code here
    pass
```

**Test Case 1:**
```python
# Example usage
nums = [1, 5, 11, 5]
result = can_partition_into_equal_sum(nums)
print("Can be Partitioned -", result)

# Expected Output: Can be partitioned - True (The set can be partitioned into [1, 5, 5] and [11])
```

**Test Case 2:**
```python
# Example usage
nums = [1, 2, 3, 4, 5, 6]
result = can_partition_into_equal_sum(nums)
print("Can be Partitioned -", result)

# Expected Output: Can be partitioned - False (No partition with equal sums is possible)
```

**Test Case 3:**
```python
# Example usage
nums = [2, 2, 2, 2, 2, 2]
result = can_partition_into_equal_sum(nums)
print("Can be Partitioned -", result)

# Expected Output: Can be partitioned - True (The set can be partitioned into [2, 2, 2] and [2, 2, 2])
```