
# [Second & Third Largest Element in Array](https://www.geeksforgeeks.org/problems/third-largest-element/1)

## Approaches
- [Approach 1: Brute Force](#approach-1-brute-force)
- [Approach 2: Better](#approach-2-better)
- [Approach 3: Optimized Single Pass](#approach-3-optimized-single-pass)

---

## Approach 1: Brute Force

### Intuition:
The brute force approach involves sorting the array and returning the elements at positions arr.length-2 & arr.length-3

### Code:
```java
public int[] secAndThirdLargest(int[] arr) {
    Arrays.sort(arr);
    return new int[]{arr.length-2,arr.length-3};
}
```
#### Complexity Analysis:
- **Time Complexity:** O(nlogn) because of sorting.
- **Space Complexity:** O(1) because no extra space is used aside from result array.

---

## Approach 2: Better

### Intuition:
We can traverse the array 3 times and find largest in the first iteration, second largest in the second iteration & third largest in the third iteration.

### Approach:

1. Initialize 3 variables largest, secLargest & thirdLargest all equal to Integer.MIN_VALUE.
2. Iterate through the array and find the largest.
3. Again iterate through the array and find the element which is just smaller than largest which will be secLargest.
4. Again iterate through the array and find the element which is just smaller than secLargest which will be thridLargest.

### Code:
```java
public int[] secAndThirdLargest(int[] arr) {
    int largest = Integer.MIN_VALUE;
    int secLargest = Integer.MIN_VALUE;
    int thirdLargest = Integer.MIN_VALUE;
    for(int ele : arr){
        if(ele > largest) largest = ele;
    }
    for(int ele : arr){
        if(ele != largest && ele > secLargest) secLargest = ele;
    }
    for(int ele : arr){
        if(ele != largest && ele != secLargest && ele > thirdLargest) thirdLargest = ele;
    }

    if(secLargest == Integer.MIN_VALUE) secLargest = -1;
    if(thirdLargest == Intger.MIN_VALUE) thirdLargest = -1;

    return new int[]{secLargest,thirdLargest};
}
```
#### Complexity Analysis:
- **Time Complexity:** O(3n) => O(n) because we iterate over the array thrice.
- **Space Complexity:** O(1) because we are not storing anything other than 3 variables which will be constant.

---

## Approach 3: Optimized Single Pass

### Intuition:
Instead of iterating the array 3 times, we can find it in one traversal by maintaining 3 variables with similar conditions as approach 2.

### Approach:

1. Initialize 3 variables largest, secLargest & thirdLargest all equal to Integer.MIN_VALUE;
2. Traverse through the array and if,
   - `arr[i] > largest` - `thirdLargest = secondLargest | secLargest = largest | largest = arr[i]`
   - `arr[i] <= largest && arr[i] > secLargest` - `thirdLargest = secLargest | secLargest = arr[i]`
   - `arr[i] <= largest && arr[i] <= secLargest && arr[i] > thirdLargest` - `thirdLargest = arr[i]`
3. After one iteration, if secLargest = Integer.MIN_VALUE (or) thirdLargest = Integer.MIN_VALUE assign -1 to it and return.

### Code:
```java
public int[] secAndThirdLargest(int[] arr) {
    int largest = Integer.MIN_VALUE;
    int secLargest = Integer.MIN_VALUE;
    int thirdLargest = Integer.MIN_VALUE;
    for(int ele : arr){
        if(ele > largest) {
          thirdLargest = secLargest;
          secLargest = largest;
          largest = ele;
        }
        else if(ele <= largest && ele > secLargest) {
          thirdLargest = secLargest;
          secLargest = ele;
        }
        else if(ele <= largest && ele <= secLargest && ele > thirdLargest) thirdLargest = ele;
    }

    if(secLargest == Integer.MIN_VALUE) secLargest = -1;
    if(thirdLargest == Integer.MIN_VALUE) thirdLargest = -1;

    return new int[]{secLargest,thirdLargest};
}
```

### Time Complexity:
- O(n) since it passes through the array once

### Space Complexity:
- O(1) because no extra space is used aside from result array & variables.

### Note:
- The above code does not check for unique elements (i.e) if arr[9,10,9,8] the above code would return [9,9]. If unique nums are needed we can modify the code as `!=` instead of `<=`. Eg: `ele != largest && ele != secLargest && ele > thirdLargest`
