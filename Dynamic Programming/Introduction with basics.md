# Introduction To Dynamic Programming

Dynamic programming (DP) is a method used in computer science and mathematics to solve complex problems by breaking them down into simpler sub-problems. It is particularly useful for optimization problems where the problem can be divided into overlapping sub-problems, which can be solved independently and combined to form the solution to the overall problem.

## Approaches

-   **Memoization:**  Known as “top-down” dynamic programming, it usually solves the problem from the main problem to the base cases.
-   **Tabulation:**  Known as “bottom-up” dynamic programming, it solves the problem from the base cases to the main problem.

## Example: Fibonacci Numbers

The Fibonacci series is as follows:

0, 1, 1, 2, 3, 5, 8, 13, 21, ...

**Find the nth Fibonacci number, where n is based on a 0-based index. Each ith number is the sum of (i-1)th and (i-2)th numbers, with the first two numbers given as 0 and 1.**

![](https://static.takeuforward.org/premium/Dynamic%20Programming/Introduction/Introduction%20to%20DP/-5hAnu_K-)

## Solution: Memoization

Memoization also known as "top-down" dynamic programming, involves solving the problem by recursively breaking it down from the main problem to the base cases and storing the results of these sub-problems in a table (usually a dictionary or an array). When the same sub-problem is encountered again, the stored result is used instead of recomputing it, thereby saving computation time.

![](https://static.takeuforward.org/premium/Dynamic%20Programming/Introduction/Introduction%20to%20DP/-cHei50YV)

### Steps to Memoize a Recursive Solution

1.  Create a dp[n+1] array initialized to -1.
2.  Check if the answer is already calculated using the dp array (dp[n] != -1). If yes, return the value.
3.  If not, compute the value and store it in the dp array before returning.

  
![](https://static.takeuforward.org/premium/Dynamic%20Programming/Introduction/Introduction%20to%20DP/-PrzKvegH)

```java
import java.util.Arrays;

public class FibonacciMemoization {
    
    // Function to calculate Fibonacci number using memoization
    public static int f(int n, int[] dp) {
        // Base case: return n if n is 0 or 1
        if (n <= 1) return n;

        // If the value is already calculated, return it
        if (dp[n] != -1) return dp[n];

        // Calculate the value and store it in dp array
        dp[n] = f(n - 1, dp) + f(n - 2, dp);
        return dp[n];
    }

    public static void main(String[] args) {
        int n = 5; // Fibonacci number to find
        int[] dp = new int[n + 1]; // Initialize dp array
        Arrays.fill(dp, -1); // Fill dp array with -1

        // Output the nth Fibonacci number
        System.out.println(f(n, dp));
    }
}

```

**Time Complexity: O(N)**  Overlapping subproblems return answers in constant time O(1). Therefore, only 'n' new subproblems are solved, resulting in O(N) complexity.

**Space Complexity: O(N)**  Using recursion stack space and an array, the total space complexity is O(N) + O(N) ≈ O(N).

## Solution: Tabulation

Tabulation, also known as "bottom-up" dynamic programming, involves solving the problem by iteratively solving all possible sub-problems, starting from the base cases and building up to the solution of the main problem. The results of sub-problems are stored in a table, and each entry in the table is filled based on previously computed entries.

### Steps to Convert Recursive Solution to Tabulation

1.  Declare a dp[] array of size n+1.
2.  Initialize base condition values, i.e., i=0 and i=1 of the dp array as 0 and 1 respectively.
3.  Use an iterative loop to traverse the array (from index 2 to n) and set each value as dp[i-1] + dp[i-2].

```java
import java.util.Arrays;

class TUF {
    public static void main(String[] args) {
        int n = 5; // Fibonacci number to find
        int dp[] = new int[n + 1]; // Initialize dp array

        dp[0] = 0; // Base case for Fibonacci sequence
        dp[1] = 1; // Base case for Fibonacci sequence

        // Fill the dp array using the tabulation method
        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }

        // Output the nth Fibonacci number
        System.out.println(dp[n]);
    }
}
```
**Time Complexity: O(N)**: Running a simple iterative loop results in O(N) complexity.

**Space Complexity: O(N)**: Using an external array of size n+1, the space complexity is O(N).

## Solution: Space Optimization

The relation dp[i] = dp[i-1] + dp[i-2] shows that only the last two values in the array are needed. By maintaining only two variables (prev and prev2), space can be optimized. This optimization reduces the space complexity from O(N) to O(1) since it eliminates the need for an entire array to store intermediate results.

In each iteration, compute the current Fibonacci number using the values of prev and prev2. Assign the value of prev to prev2 and the value of the current Fibonacci number to prev. This way, the variables are updated for the next iteration. After the loop completes, the variable prev holds the value of the nth Fibonacci number, which is then returned as the result.

![](https://static.takeuforward.org/premium/Dynamic%20Programming/Introduction/Introduction%20to%20DP/-E89DlZxw)

```java
public class Fibonacci {
    public static void main(String[] args) {
        int n = 5; // Fibonacci number to find

        // Edge case: if n is 0, the result is 0
        if (n == 0) {
            System.out.println(0);
            return;
        }

        // Edge case: if n is 1, the result is 1
        if (n == 1) {
            System.out.println(1);
            return;
        }

        int prev2 = 0; // Fibonacci number for n-2
        int prev = 1;  // Fibonacci number for n-1

        // Iterate from 2 to n to find the nth Fibonacci number
        for (int i = 2; i <= n; i++) {
            int cur_i = prev2 + prev; // Current Fibonacci number
            prev2 = prev;             // Update prev2 to the previous Fibonacci number
            prev = cur_i;             // Update prev to the current Fibonacci number
        }

        // Print the nth Fibonacci number
        System.out.println(prev);
    }
}

```
**Time Complexity** O(N) : We are running a simple iterative loop

**SpaceComplexity** O(1) : We are not using any extra space

## Conclusion

Dynamic programming is a powerful technique for solving complex problems by breaking them down into simpler subproblems. By using approaches like memoization and tabulation, it is possible to optimize both time and space complexities. Understanding the principles behind dynamic programming and practicing with examples like the Fibonacci sequence can help in mastering this method.

## Additional Information

Dynamic programming problems can often be identified by the presence of overlapping subproblems and optimal substructure properties. Overlapping subproblems mean that the same subproblems are solved multiple times, and optimal substructure means that the solution to a problem can be composed of solutions to its subproblems. Common applications of dynamic programming include problems related to sequences, such as the longest common subsequence, and optimization problems, such as the knapsack problem.


