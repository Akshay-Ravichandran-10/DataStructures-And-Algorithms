# [Maximum & Minimum in an Array](https://www.geeksforgeeks.org/problems/find-minimum-and-maximum-element-in-an-array4428/1)

## Table of Contents
1. [Brute Force Approach](#brute-force-approach)
2. [Optimized One Pass Approach](#optimized-one-pass-approach)

### Brute Force Approach

### Intuition:

The problem requires us to find the maximum & minimum element in the array. Using a brute force approach, we can sort the array and return the elements at 0 index & last index of the array.

### Approach:

1. Sort the array.
2. Return the elements at arr[0] & arr[arr.length-1]

#### Complexity Analysis:
- **Time Complexity:** O(nlogn) due to sorting.
- **Space Complexity:** O(1) as no extra space is used.

```java
public class Solution {
    public int[] maxAndMin(int[] arr) {
        Arrays.sort(arr);
        return new int[]{arr[0],arr[arr.length-1]};
    }
}
```

---

### Optimized One Pass Approach

### Intuition:

Instead of sorting the array. We can traverse through the array to find the maximum & minimum element possible.

### Approach:

1. Initialize variables for tracking the maximum & minimum element seen so far (`maximum`) and (`minimum`) both initialized to Integer.MIN_VALUE & Integer.MAX_VALUE respectively.
2. Iterate through the array.
3. For each element:
   - Update the `maximum` if the current element is greater than the `maximum`.
   - Update the `minimum` if the current element is less than the `minimum`.
4. Return `maximum` & `minimum` after processing all elements.

#### Complexity Analysis:
- **Time Complexity:** O(n) since we only pass through the array once.
- **Space Complexity:** O(1) as no additional space is required beyond a few variables.

```java
public class Solution {
    public int[] maxAndMin(int[] arr) {
        int maximum = Integer.MIN_VALUE;
        int minimum = Integer.MAX_VALUE;
        for(int ele : arr){
            if(ele > maximum) maximum = ele;
            if(ele < minimum) minimum = ele;
        }
        return new int[]{maximum,minimum};
    }
}
```

In summary, while the brute force approach provides a straightforward solution through sorting, the optimized one-pass approach efficiently finds the maximum & minimum elements by utilizing the concept of maintaining both values seen thus far with constant space and linear time complexity.
