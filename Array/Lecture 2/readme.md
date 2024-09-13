# Lecture Day 2

## Question 1a: 
Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search target in nums. If target exists, then return its index. Otherwise, return -1.

You must write an algorithm with O(log n) runtime complexity.

Example 1:
```
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
```

Example 2:
```
Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1
```

Constraints:

- `1 <= nums.length <= 10e4`
- `-1e4 < nums[i], target < 1e4`
- All the integers in `nums` are unique.
- `nums` is sorted in ascending order

**Follow up:** Can you solve the problem in `O(log(n))` time complexity?

<!-- ## Solution 

**Intuition and Approach:**

The problem involves searching for a target value in a sorted integer array. Here's how the two provided solutions tackle this:

**1. Linear Search (`linear_search`):**

   - **Intuition:** This method iterates through the array from the beginning to the end, checking each element against the target value. It returns the index of the target value if found, otherwise returns -1.
   - **Approach:**
      ```
      FUNCTION linear_search(arr, size, target)
         FOR i FROM 0 TO size - 1
            IF arr[i] == target
               RETURN i
            END IF
         END FOR
         RETURN -1  // Target not found
      END FUNCTION
      ```

**2. Binary Search (`binary_search`):**

   - **Intuition:** This method leverages the fact that the array is sorted. It repeatedly divides the search interval in half, comparing the middle element with the target value. Depending on the comparison, it eliminates half of the remaining elements from consideration.
   - **Approach:**
      ```
      FUNCTION binary_search(arr, size, target)
         left = 0
         right = size - 1
         WHILE left <= right
            mid = left + (right - left) / 2
            IF arr[mid] == target
               RETURN mid
            ELSE IF arr[mid] > target
               right = mid - 1
            ELSE
               left = mid + 1
            END IF
         END WHILE
         RETURN -1  // Target not found
      END FUNCTION
      ```

**Key Differences and Considerations:**

- **Time Complexity:**
   - Linear Search: `O(n)` due to iterating through each element of the array.
   - Binary Search: `O(log n)` due to repeatedly dividing the search interval in half.

- **Space Complexity:**
   - Both solutions: `O(1)` as they only use a few extra variables for tracking indices and comparisons.

**Choosing the Right Approach:**

- Use linear search for small or unsorted arrays where the overhead of sorting or maintaining a sorted array is not justified.
- Use binary search for large, sorted arrays where the target value can be quickly found due to the logarithmic time complexity.
 -->

## Question 1b: 
There is an integer array `nums` sorted in ascending order (with distinct values).

Prior to being passed to your function, `nums` is possibly rotated at an unknown pivot index `k` (`1 <= k < nums.length`) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` **(0-indexed)**. For example, `[0,1,2,4,5,6,7]` might be rotated at pivot index `3` and become `[4,5,6,7,0,1,2]`.

Given the array `nums` after the possible rotation and an integer `target`, return the index of `target` if it is in `nums`, or `-1` if it is not in `nums`.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**
```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```
**Example 2:**
```
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```
**Example 3:**
```
Input: nums = [1], target = 0
Output: -1
```
**Constraints:**

- `1 <= nums.length <= 5000`
- `-1e4 <= nums[i] <= 1e4`
- All values of `nums` are unique.
- `nums` is an ascending array that is possibly rotated.
- `-1e4 <= target <= 1e4`

**Follow up:** Can you solve the problem in `O(log(n))` time complexity?

<!-- ## Solution 
**Intuition and Approach:**

The problem involves searching for a target value in a rotated sorted integer array. Here's how the two provided solutions tackle this:

**1. Linear Search (`linear_search`):**

   - **Intuition:** This method iterates through the array from the beginning to the end, checking each element against the target value. It returns the index of the target value if found, otherwise returns -1.
   - **Approach:**
      ```
      FUNCTION linear_search(arr, size, target)
         FOR i FROM 0 TO size - 1
            IF arr[i] == target
               RETURN i
            END IF
         END FOR
         RETURN -1  // Target not found
      END FUNCTION
      ```

**2. Rotational Binary Search (`rotational_binary_search`):**

   - **Intuition:** This approach leverages the fact that the array is a rotated sorted array. It modifies the traditional binary search to handle the rotation by checking which half of the array is properly sorted and adjusting the search interval accordingly.
   - **Approach:**
      ```
      FUNCTION rotational_binary_search(arr, size, target)
         left = 0
         right = size - 1
         WHILE left <= right
            mid = left + (right - left) / 2
            IF arr[mid] == target
               RETURN mid
            END IF
            // Determine which part of the array is sorted
            IF arr[left] <= arr[mid]
               // Left part is sorted
               IF arr[left] <= target AND target < arr[mid]
                  right = mid - 1
               ELSE
                  left = mid + 1
               END IF
            ELSE
               // Right part is sorted
               IF arr[mid] < target AND target <= arr[right]
                  left = mid + 1
               ELSE
                  right = mid - 1
               END IF
            END IF
         END WHILE
         RETURN -1  // Target not found
      END FUNCTION
      ```

**Key Differences and Considerations:**

- **Time Complexity:**
   - Linear Search: `O(n)` due to iterating through each element of the array.
   - Rotational Binary Search: `O(log n)` due to repeatedly dividing the search interval in half and handling the rotation.

- **Space Complexity:**
   - Both solutions: `O(1)` as they only use a few extra variables for tracking indices and comparisons.

**Choosing the Right Approach:**

- Use linear search for small or unsorted arrays where the overhead of sorting or maintaining a sorted array is not justified.
- Use rotational binary search for large, rotated sorted arrays where the target value can be quickly found due to the logarithmic time complexity. -->

## Question 2: 
Given an integer array `nums`, find a peak element. A peak element is an element that is not smaller than its neighbors. If the array contains multiple peaks, return the index to any one of the peaks.

**Input:**
- An integer array `nums` where `1 <= nums.length <= 10^5`.
- Each element `nums[i]` is an integer where `-10^4 <= nums[i] <= 10^4`.

**Output:**
- An integer representing the index of a peak element.

**Notes:**
- `nums[-1]` and `nums[n]` are considered to be negative infinity (`-∞`).

**Example 1:**
```
Input: nums = [1, 2, 3, 1]
Output: 2
Explanation: 3 is a peak element and your function should return the index number 2.
```

**Example 2:**
```
Input: nums = [1, 2, 1, 3, 5, 6, 4]
Output: 1 or 5
Explanation: Your function can return index number 1 where the peak element is 2, or index number 5 where the peak element is 6.
```

**Follow up:** Your solution should run in O(log n) time complexity.

<!-- ## Solution 

**Intuition and Approach:**

The problem involves finding a peak element in a given integer array, where a peak element is an element that is greater than its neighbors. Here's how the two provided solutions tackle this:

**1. Brute Force Approach (`bruteForce_peak_element`):**

   - **Intuition:** This method iterates through the array, keeping track of the maximum value and its index. By the end of the iteration, the index of the maximum value is returned as the peak element.
   - **Approach:**
      ```
      FUNCTION bruteForce_peak_element(nums)
         length = size of nums
         max = nums[0]
         res = 0
         FOR i FROM 1 TO length - 1
            IF max < nums[i]
               max = nums[i]
               res = i
            END IF
         END FOR
         RETURN res
      END FUNCTION
      ```

**2. Optimal Solution (`optimal_peak_element`):**

   - **Intuition:** This approach uses a modified binary search to find a peak element efficiently. It repeatedly divides the search interval in half, comparing the middle element with its neighbors to determine the direction in which a peak exists.
   - **Approach:**
      ```
      FUNCTION optimal_peak_element(nums)
         low = 0
         high = size of nums - 1

         // Check if there's only one element
         IF high == 0
            RETURN low

         // Check the boundary elements
         IF nums[low] > nums[low + 1]
            RETURN low
         IF nums[high] > nums[high - 1]
            RETURN high

         // Narrow the search range
         low = low + 1
         high = high - 1

         WHILE low <= high
            mid = (high + low) / 2

            // Check if mid is a peak
            IF nums[mid] > nums[mid - 1] AND nums[mid] > nums[mid + 1]
               RETURN mid

            // Move to the right half
            IF nums[mid] > nums[mid - 1]
               low = mid + 1
            ELSE
               high = mid - 1
         END WHILE

         RETURN -1  // No peak element found
      END FUNCTION
      ```

**Key Differences and Considerations:**

- **Time Complexity:**
   - Brute Force: `O(n)` due to iterating through each element of the array.
   - Optimal: `O(log n)` due to repeatedly dividing the search interval in half.

- **Space Complexity:**
   - Both solutions: `O(1)` as they only use a few extra variables for tracking indices and comparisons.

**Choosing the Right Approach:**

- Use the brute force approach for small arrays or when a simple implementation is preferred.
- Use the optimal approach for large arrays to take advantage of the logarithmic time complexity for efficient peak element finding. -->

## Question 3: 
Given an array `nums` sorted in non-decreasing order, return the maximum between the number of positive integers and the number of negative integers.

In other words, if the number of positive integers in `nums` is `pos` and the number of negative integers is `neg`, then return the maximum of `pos` and `neg`.

**Note** that `0` is neither positive nor negative.

**Example 1:**
```
Input: nums = [-2,-1,-1,1,2,3]
Output: 3
Explanation: There are 3 positive integers and 3 negative integers. The maximum count among them is 3.
```
**Example 2:**
```
Input: nums = [-3,-2,-1,0,0,1,2]
Output: 3
Explanation: There are 2 positive integers and 3 negative integers. The maximum count among them is 3.
```
**Example 3:**
```
Input: nums = [5,20,66,1314]
Output: 4
Explanation: There are 4 positive integers and 0 negative integers. The maximum count among them is 4.
```
 
**Constraints:**

- `1 <= nums.length <= 2000`
- `-2000 <= nums[i] <= 2000`
- `nums` is sorted in a non-decreasing order.


**Follow up:** Can you solve the problem in `O(log(n))` time complexity?

<!-- ## Solution
**Intuition and Approach:**

The problem involves counting the number of positive and negative numbers in a sorted integer array. Here's how the two provided solutions tackle this:

**1. Brute Force Approach (`bruteForce_sum_neg`):**

   - **Intuition:** This method iterates through the array, checking each element to count the number of positive and negative numbers.
   - **Approach:**
      ```
      FUNCTION bruteForce_sum_neg(nums)
         pos = 0
         neg = 0
         FOR num IN nums
            IF num > 0
               pos = pos + 1
            ELSE IF num < 0
               neg = neg + 1
            END IF
         END FOR
         RETURN (pos, neg)
      END FUNCTION
      ```

**2. Optimal Solution (`optimal_sum_neg`):**

   - **Intuition:** This approach leverages the fact that the array is sorted to use binary search for efficiently finding the boundaries between negative, zero, and positive numbers.
   - **Approach:**
      ```
      FUNCTION optimal_sum_neg(nums)
         size = size of nums
         
         // Handle edge cases
         IF nums[0] > 0
            RETURN (size, 0)  // All numbers are positive
         IF nums[size - 1] < 0
            RETURN (0, size)  // All numbers are negative
         IF nums[0] == 0 AND nums[size - 1] == 0
            RETURN (0, 0)  // All numbers are zero
         
         lastNeg = -1
         firstPos = size
         
         // Find the last negative number
         left = 0
         right = size - 1
         WHILE left <= right
            mid = left + (right - left) / 2
            IF nums[mid] < 0
               IF mid + 1 < size AND nums[mid + 1] >= 0
                  lastNeg = mid
                  BREAK
               END IF
               left = mid + 1
            ELSE
               right = mid - 1
            END IF
         END WHILE
         
         // Find the first positive number
         left = 0
         right = size - 1
         WHILE left <= right
            mid = left + (right - left) / 2
            IF nums[mid] > 0
               IF mid - 1 >= 0 AND nums[mid - 1] <= 0
                  firstPos = mid
                  BREAK
               END IF
               right = mid - 1
            ELSE
               left = mid + 1
            END IF
         END WHILE
         
         posCount = size - firstPos
         negCount = lastNeg + 1
         
         RETURN (posCount, negCount)
      END FUNCTION
      ```

**Key Differences and Considerations:**

- **Time Complexity:**
   - Brute Force: `O(n)` due to iterating through each element of the array.
   - Optimal: `O(log n)` due to using binary search to find the boundaries between negative and positive numbers.

- **Space Complexity:**
   - Both solutions: `O(1)` as they only use a few extra variables for tracking indices and counts.

**Choosing the Right Approach:**

- Use the brute force approach for small arrays or when a simple implementation is preferred.
- Use the optimal approach for large arrays to take advantage of the logarithmic time complexity for efficient counting. -->

## Question 4:
Given an array of strings, group the anagrams together. You can return the answer in any order.

**Input:**
- An array of strings `strs` 
- where `1 <= len(strs) <= 1e5`
- each string `s` where `1 <= len(s) <= 100`.

**Output:**
- A list of lists, where each sublist contains strings that are anagrams of each other.

**Example 1:**
```
Input: strs = ["eat", "tea", "tan", "ate", "nat", "bat"]
Output: [["eat", "tea", "ate"], ["tan", "nat"], ["bat"]]
```

**Example 2:**
```
Input: strs = ["listen", "silent", "enlist", "inlets", "google", "goolge"]
Output: [["listen", "silent", "enlist", "inlets"], ["google", "goolge"]]
```

<!-- ## Solution

**Intuition and Approach:**

The problem is to group anagrams from a list of strings. An anagram is a word formed by rearranging the letters of another word. Here's how the two provided solutions tackle this problem:

**1. Using Hashmap (`groupAnagrams1`):**

   - **Intuition:** By sorting each string, we can use the sorted string as a key to group anagrams together.
   - **Approach:**
      ```
      FUNCTION groupAnagrams1(strs)
         DECLARE anagramMap as a hashmap

         FOR each str IN strs
            sortedStr = SORTED str
            anagramMap[sortedStr].ADD str
         END FOR

         DECLARE result as an empty list
         FOR each pair IN anagramMap
            ADD pair.second to result
         END FOR

         RETURN result
      END FUNCTION
      ```

**2. Without Using Hashmap (`groupAnagrams2`):**

   - **Intuition:** By sorting each string and maintaining both the original and sorted versions, we can sort this list and then group anagrams based on the sorted strings.
   - **Approach:**
      ```
      FUNCTION groupAnagrams2(strs)
         DECLARE sortedStrs as an empty list

         FOR each str IN strs
            sortedStr = SORTED str
            ADD (sortedStr, str) to sortedStrs
         END FOR

         SORT sortedStrs based on the first element of each pair

         DECLARE result as an empty list
         DECLARE currentGroup as an empty list
         currentKey = first element of the first pair in sortedStrs

         FOR each pair IN sortedStrs
            IF pair.first EQUALS currentKey
               ADD pair.second to currentGroup
            ELSE
               ADD currentGroup to result
               currentGroup = [pair.second]
               currentKey = pair.first
            END IF
         END FOR

         ADD currentGroup to result
         RETURN result
      END FUNCTION
      ```

**Key Differences and Considerations:**

- **Time Complexity:**
   - Using Hashmap: Sorting each string takes `O(k log k)` where `k` is the length of the string. The overall complexity is `O(n k log k)` where `n` is the number of strings.
   - Without Hashmap: Similar sorting complexity `O(n k log k)` but includes additional sorting of the pairs `O(n log n)`.

- **Space Complexity:**
   - Using Hashmap: `O(n k)` due to the hashmap storing all strings.
   - Without Hashmap: `O(n k)` due to the list of pairs.

**Choosing the Right Approach:**

- The hashmap approach (`groupAnagrams1`) is more intuitive and straightforward, especially when dealing with large datasets.
- The non-hashmap approach (`groupAnagrams2`) can be useful in environments where hashmaps are not available or preferred. -->
