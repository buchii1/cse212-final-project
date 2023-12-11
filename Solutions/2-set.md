# Solution to Set Assignment

Below is the solution to the `can_partition_into_equal_sum` problem:

```python
def can_partition_into_equal_sum(nums):
    # Calculate the total sum of the numbers in the input list
    total_sum = sum(nums)

    # If the total sum is odd, the set cannot be partitioned into two subsets with equal sums
    if total_sum % 2 != 0:
        return False

    # Calculate the target sum for each subset
    target_sum = total_sum // 2

    # Initialize a dynamic programming array to track feasibility of achieving each sum
    dp = [False] * (target_sum + 1)
    
    # There is always one way to achieve a sum of 0 (empty subset)
    dp[0] = True

    # Iterate through each number in the input list
    for num in nums:
        # Iterate from the target sum down to the current number
        for i in range(target_sum, num - 1, -1):
            # Update dp[i] if either dp[i] or dp[i - num] is True
            dp[i] = dp[i] or dp[i - num]

    # The final result is whether the target sum can be achieved using a subset of the given numbers
    return dp[target_sum]
```