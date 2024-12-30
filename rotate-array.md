# [Leetcode 189: Rotate Array](https://leetcode.com/problems/rotate-array/)

## Approaches

- [Approach 1: Extra Array for New Order](#approach-1-extra-array-for-new-order)
- [Approach 2: Do Rotate By One for K times](#approach-2-do-rotate-by-one-for-k-times)
- [Approach 3: Reverse the Array](#approach-3-reverse-the-array)

---

## Approach 1: Extra Array for New Order

### Intuition
By using an additional array, you can directly place each element in its rotated position. This avoids costly movement within the original array but requires additional space for storing the results.

### Steps
1. Create a new array to hold rotated elements.
2. Calculate and place each element in its final position.
3. Copy the result back into the original array.

```java
class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        int[] rotated = new int[n];
        k = k % n; // Handle cases where k >= n
        
        // Place elements in the new positions
        for (int i = 0; i < n; i++) {
            rotated[(i + k) % n] = nums[i];
        }
        
        // Copy the content of rotated array to the original array
        for (int i = 0; i < n; i++) {
            nums[i] = rotated[i];
        }
    }
}
```

**Time Complexity:** O(n) - Each element is processed a constant number of times.

**Space Complexity:** O(n) - Additional array to hold rotated order.

---

## Approach 2: Do Rotate By One for K times

### Intuition
Rotating the array by one postion shifts the array elements by one place, hence doing for k times in a loop will give the required output.

### Steps
1. Take the last element and place it in a 'temp' variable
2. Shift the elements one position to right.
3. Then place the 'temp' value in first index.
4. Repeat the above steps for k times

```java
class Solution {
    public void rotate(int[] nums, int k) {
        if(nums.length < k) k = k % nums.length;
        for(int i=0; i<k; i++){
            rotateOneTime(nums);
        }
    }

    public void rotateOneTime(int[] nums){
        int temp = nums[nums.length - 1];
        for(int i=nums.length-2; i>=0; i--){
            nums[i+1] = nums[i];
        }
        nums[0] = temp;
    }
}
```

**Time Complexity:** O(n*k) - Shifting all the array elements except one for K times.

**Space Complexity:** O(1) - No additional space is used.

---

## Approach 3: Reverse the Array

### Intuition
The optimal solution utilizes array reversing. The underlying idea is that rotating an array is equivalent to reversing parts of the array. Specifically:
1. Reverse the entire array.
2. Reverse the first `k` elements.
3. Reverse the elements from `k` to the end.

### Steps
1. Reverse the whole array.
2. Reverse the first `k` elements.
3. Reverse the remaining `n-k` elements.

### Explanation
- Reversing the array repositions elements such that their relative distance with respect to rotation is preserved.
- Reversing segments then readjusts their final positions.

```java
class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        k = k % n; // Handle cases where k >= n
        
        // Step 1: Reverse the whole array
        reverse(nums, 0, n - 1);
        // Step 2: Reverse the first k elements
        reverse(nums, 0, k - 1);
        // Step 3: Reverse the remaining elements
        reverse(nums, k, n - 1);
    }

    private void reverse(int[] nums, int start, int end) {
        while (start < end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
}
```

**Time Complexity:** O(n) - Each reverse operation is O(n), and we perform a constant number of them.

**Space Complexity:** O(1) - Reversal done in-place without extra space.
