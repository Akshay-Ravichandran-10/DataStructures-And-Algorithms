# [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

## Table of Contents
1. [Brute Force Approach](#brute-force-approach)
2. [Optimized One Pass Approach](#optimized-one-pass-approach)

### Brute Force Approach

**Intuition:**

The problem requires us to find the maximum profit possible from a series of stock prices where you can buy and sell once. Using a brute force approach, we can try all possible combinations of buying and selling days and compute the profit for each combination. The maximum of these profits will be our answer.

**Approach:**

1. Iterate through the list of prices with two nested loops.
2. The outer loop will represent the buying day.
3. The inner loop will represent the selling day.
4. For each combination of buying and selling days, calculate the profit.
5. Maintain a variable to keep track of the maximum profit observed.

**Time Complexity:** O(n^2) due to the two nested loops.
**Space Complexity:** O(1) as no extra space is used.

```java
public class Solution {
    public int maxProfit(int[] prices) {
        int maxResult = 0;
        //Check all buying days
        for(int i=0; i<prices.length; i++){
            //Check all selling days
            for(int j=i+1; j<prices.length; j++){
                //Check only if selling day > buying day
                if(prices[j] > prices[i]){
                    maxResult = Math.max(maxResult,prices[j]-prices[i]);
                }
            }
        }
        return maxResult;
    }
}
```

---

### Optimized One Pass Approach

**Intuition:**

Instead of trying all possible pairs of buy and sell days, we can iterate through the list of prices once while keeping track of the minimum price encountered so far. At each step, we calculate what the profit would be if we sold at the current price, and update the maximum profit correspondingly.

**Approach:**

1. Initialize variables for tracking the minimum price seen so far (`minPrice`) and maximum profit (`maxResult`).
2. Iterate through the prices.
3. For each price:
   - Update the `minPrice` if the current price is lower than the `minPrice`.
   - Calculate the profit if the stock were sold today.
   - Update `maxResult` if the calculated profit is greater than `maxProfit`.
4. Return `maxResult` after processing all prices.

**Time Complexity:** O(n) since we only pass through the prices array once.
**Space Complexity:** O(1) as no additional space is required beyond a few variables.

```java
public class Solution {
    public int maxProfit(int[] prices) {
        int maxResult = 0;
        int minPrice = Integer.MAX_VALUE;
        for(int i=0; i<prices.length; i++){
            minPrice = Math.min(prices[i],min);
            maxResult = Math.max(maxResult,prices[i]-minPrice);
        }
        return maxResult;
    }
}
```

In summary, while the brute force approach provides a straightforward solution through trial and error, the optimized one-pass approach efficiently finds the maximum profit by utilizing the concept of maintaining minimum values seen thus far with constant space and linear time complexity.
