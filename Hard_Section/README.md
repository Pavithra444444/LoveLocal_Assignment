## **Hard 2**
You are given a string s. You can convert s to a palindrome by adding characters in front of it.Return the shortest palindrome you can find by performing this transformation.

*Solution:*
~~~
class Solution:
    def shortestPalindrome(self, s: str) -> str:
        i = 0
        n = len(s)
        for j in range(n):
            if s[i] == s[n-j-1]:
                i += 1
        if i==n:
            return s
        p = s[i:n][::-1]
        return p + self.shortestPalindrome(s[:i]) + s[i:]
~~~

**Logic and Algorithm Explanation:**

This code implements a KMP-inspired algorithm to find the shortest palindrome string that can be formed by adding characters to the beginning of the original string. Here's a breakdown of the logic and algorithm:

1. Finding the Longest Palindrome Prefix:

The code iterates over the string s using two variables: i and j.
i tracks the length of the longest prefix found so far.
j starts from the end of the string and moves towards the beginning.
At each iteration, the code compares the characters at positions i and n-j-1.
If the characters are equal, i is incremented, indicating the prefix has grown by one character.
This loop essentially finds the longest palindromic prefix within the original string.

2. Checking for Full Palindrome:

If i reaches the length of the string (n), it implies the entire string is already a palindrome and no additional characters are needed. The original string is returned in this case.

3. Building the Suffix String:

If the entire string is not a palindrome, a suffix string p is constructed.
This string is the reversed substring of s starting from the position i until the end (excluding the character at i).
This suffix string essentially contains the "missing" characters needed to complete the palindrome.

4. Recursive Call:

The code then performs a recursive call to the shortestPalindrome function, passing two substrings:
s[:i]: the prefix of the original string up to the identified length of the longest palindrome prefix.
s[i:]: the remaining substring of the original string.

5. Combining the Substrings:

The result of the recursive call is appended to the previously constructed suffix string p.
Finally, this combined string is concatenated with the original string and returned.

Overall Algorithm:

Find the longest palindrome prefix in the string.
Check if the entire string is already a palindrome.
If not, build a suffix string containing the "missing" characters.
Recursively call the function on the remaining substring.
Combine the results and return the shortest palindrome.

Time Complexity:

The time complexity of this algorithm is O(n), where n is the length of the input string. This is due to the single loop and the efficient use of recursion.

Space Complexity:

The space complexity is also O(n), considering the storage for the suffix string and the call stack during recursion.

## **Hard 3**
Given an integer n, count the total number of digit 1 appearing in all non-negative integers less than or equal to n.

*Solution:*

~~~
class Solution:
    def countDigitOne(self, n: int) -> int:
        def count(add,n_digit):
            c = 0
            for d in range(0,n_digit+1):
                c += (d+add)*math.comb(n_digit,d)*9**(n_digit-d)
            return c
        res = 0
        n_list = [int(x) for x in str(n)]
        count_1 = 0
        for i in range(len(n_list)-1):
            if n_list[i] == 1:
                res += count(count_1,len(n_list)-i-1)
                count_1 += 1
            elif n_list[i] > 1:
                leading = n_list[i]-1
                res += count(count_1,len(n_list)-i-1)*leading+count(count_1+1,len(n_list)-i-1)
        res += count_1*(n_list[-1]+1)
        if n_list[-1] >= 1:
            res += 1
        return res
~~~

**Logic and Algorithm Explanation:**

This code defines a function countDigitOne that takes an integer n as input and returns the total number of occurrences of the digit 1 in all non-negative integers less than or equal to n. Here's a breakdown of the logic and algorithm:

1. Function count:

An inner function count is defined to calculate the number of occurrences of the digit 1 considering a specific digit at the beginning (add) and the number of digits (n_digit).
It utilizes the following steps:
Iterates from 0 to n_digit+1.
For each digit (d) within the loop, calculates the contribution to the count using the formula:
(d+add)*math.comb(n_digit,d)*9**(n_digit-d)
This formula considers the possibilities of having 0, 1, or 2 occurrences of the digit 1 within the n_digit digits.
Finally, the function returns the cumulative count for all possibilities.

2. Main Function:

The main function countDigitOne iterates through the digits of n from most significant to least significant bit.
It defines two variables:
count_1: tracks the number of occurrences of the digit 1 encountered so far.
res: accumulates the total count of 1s.
Inside the loop:
Check the current digit:
If it's 1, update res using the count function with appropriate parameters.
If it's greater than 1, update res based on the number of leading digits and potential occurrences of 1s.
Finally, the function includes the contribution of the least significant digit and adds 1 if it's 1.

Overall Algorithm:

Define a function count to calculate the number of occurrences of 1 considering a specific digit at the beginning and the number of digits.
Iterate through the digits of n from most to least significant.
Update the total count (res) based on the current digit and accumulated occurrences of 1s.
Include the contribution of the least significant digit and return the final count.

Time Complexity:

The time complexity of this algorithm is O(log n). This is because the number of iterations is proportional to the number of digits in n.

Space Complexity:

The space complexity is O(1) as it only uses a constant amount of additional memory for temporary variables.
