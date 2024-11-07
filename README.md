# Add Two Numbers - Leetcode Problem

## Problem Description

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except for the number 0 itself.

### Example 1:
![image](https://github.com/user-attachments/assets/dd812ed6-3f2a-4510-b635-517f77a04de3)

**Input:**  
`l1 = [2,4,3]`, `l2 = [5,6,4]`  
**Output:**  
`[7,0,8]`  
**Explanation:**  
342 + 465 = 807.

### Example 2:
**Input:**  
`l1 = [0]`, `l2 = [0]`  
**Output:**  
`[0]`

### Example 3:
**Input:**  
`l1 = [9,9,9,9,9,9,9]`, `l2 = [9,9,9,9]`  
**Output:**  
`[8,9,9,9,0,0,0,1]`

### Constraints:
- The number of nodes in each linked list is in the range `[1, 100]`.
- `0 <= Node.val <= 9`
- It is guaranteed that the list represents a number that does not have leading zeros.


## We will look at 2 approaches to solve this problem

## Approach 1

We can solve this problem using two approaches:

### 1. Using Reverse Lists and String Summation

The first approach involves reversing both input lists, converting them to numbers, summing them, and then reversing the result. However, this approach uses multiple loops, which can be inefficient.

### Steps:
1. Reverse the first input array and sum it.
2. Reverse the second input array and sum it.
3. Add the two sums.
4. Reverse the final sum.

### Code Implementation:
```dart
void main() {
    List<int> l1 = [2, 4, 3]; // First input list
    String l1Sum = ''; // Will store the reversed first input value
    
    List<int> l2 = [5, 6, 4]; // Second input list
    String l2Sum = ''; // Will store the reversed second input value
    
    List<int> outputArr = []; // Will store the final output
    String summarySum = ''; // Will store the sum of the two reversed inputs

    for (int a = l1.length - 1; a >= 0; a--) {
        l1Sum += l1[a].toString(); // Reverse and sum first list
    }

    for (int a = l2.length - 1; a >= 0; a--) {
        l2Sum += l2[a].toString(); // Reverse and sum second list
    }

    print('sum l1: $l1Sum'); // Output will be 342
    print('sum l2: $l2Sum'); // Output will be 465
    
    summarySum = (int.parse(l1Sum) + int.parse(l2Sum)).toString(); // Sum the two values
    print('sum: $summarySum'); // Output will be 807
    
    for (int a = summarySum.length - 1; a >= 0; a--) { // Reverse the final sum
        outputArr.add(int.parse(summarySum[a].toString()));
    }
    
    print(outputArr); // Output will be [7, 0, 8]
}
```

## 

# Optimized Approach for Adding Two Numbers Represented by Lists

## Problem with the Initial Approach

The initial solution involves three loops and string manipulations, making it inefficient, especially for larger inputs. It involves reversing the lists, converting them to strings, and then adding them, which increases both time and space complexity.

## Optimized Approach: Direct Summation with Carry

In the optimized approach, we sum the digits directly from left to right, handling the carry at each step. This approach only requires one loop, making it more efficient.

### Steps

1. Traverse both lists from left to right.
2. Sum the corresponding digits along with any carry from the previous step.
3. Store the result as the last digit of the sum.
4. If there's any carry left after traversing both lists, add it as the last digit.

### Code Implementation

```dart
void main() {
    List<int> l1 = [2, 4, 3]; // Represents 342
    List<int> l2 = [5, 6, 4]; // Represents 465
    List<int> outputArr = []; // Will store the final result
    
    int maxLength = l1.length > l2.length ? l1.length : l2.length;
    int carry = 0;

    for (int i = 0; i < maxLength; i++) {
        int val1 = i < l1.length ? l1[i] : 0;
        int val2 = i < l2.length ? l2[i] : 0;
        
        int sum = val1 + val2 + carry;
        
        // Add the current digit to the result (sum modulo 10)
        outputArr.add(sum % 10);
        
        // Determine the carry using integer division
        carry = sum >= 10 ? (sum / 10).toInt() : 0;  // Convert to int to discard the decimal part
    }

    if (carry > 0) {
        outputArr.add(carry);
    }

    print(outputArr); // Output: [7, 0, 8] for [2, 4, 3] + [5, 6, 4]
}


```
# Optimized Approach for Adding Two Numbers Represented by Lists

## Explanation

In this approach, we iterate through both lists, summing the corresponding digits along with any carry from the previous step.

- If the sum of two digits and the carry exceeds 9, we take the remainder (`sum % 10`) as the current digit, and the carry for the next iteration is calculated.
- After the loop finishes, if there is any carry left, it is added as the last digit.

For example, with the input lists:
- `l1 = [2, 4, 3]` (represents the number 342)
- `l2 = [5, 6, 4]` (represents the number 465)

The output will be `[7, 0, 8]`, which corresponds to the number `807`.

## Time Complexity

- **Reverse and Sum Approach**: The time complexity is `O(n + m)`, where `n` and `m` are the lengths of the two lists. This includes the time for reversing the lists (`O(n)`) and summing the digits (`O(m)`).
- **Optimized Approach**: The time complexity is `O(n)`, where `n` is the length of the longer list. We traverse each list once and handle carry in constant time.

## Space Complexity

- **Reverse and Sum Approach**: The space complexity is `O(n + m)` due to string manipulations and the final result list storage.
- **Optimized Approach**: The space complexity is `O(max(n, m))` as we only store the result in the output list.

## Conclusion

The optimized approach reduces both time and space complexity significantly. It is much faster and more efficient, especially for larger inputs, and is preferred over the reverse and sum approach.


