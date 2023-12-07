**Easy 1**

Given a string s consisting of words and spaces, return the length of the last word in the string.

A word is a maximal substring consisting of non-space characters only.

Solution:

  class Solution:
  
      def lengthOfLastWord(self, s: str) -> int:
          res=s.split()
          return len(res[-1])

Logic and Algorithm Explanation

The provided code defines a function lengthOfLastWord that takes a string s as input and returns the length of the last word in the string. The logic and algorithm implemented are as follows:

1. Splitting the string:

The code uses the split() method on the string s with a single space (" ") as the delimiter. This method creates a list of strings, with each element representing a separate word separated by spaces.

2. Accessing the last element:

Since we're interested in the last word, we access the last element of the list using res[-1]. This element will be the string representing the last word in the original input string.

3. Returning the length:

Finally, we use the len() function to get the length of the last word string and return it.

Overall Algorithm:

Split the input string into a list of words using split().
Access the last element of the list (last word).
Return the length of the last word using len().

Time Complexity:

The time complexity of this algorithm is O(n), where n is the length of the input string. This is because the split() method takes linear time in the worst case.

Space Complexity:

The space complexity of this algorithm is also O(n), as it creates a new list containing all the words in the original string.

**Easy  2**

Given an integer array nums where the elements are sorted in ascending order, convert it to a 
height-balanced binary search tree.   

Solution:

class Solution:

    def sortedArrayToBST(self, nums: List[int]) -> Optional[TreeNode]:
        total_nums = len(nums)
        if not total_nums:
            return None

        mid_node = total_nums // 2
        return TreeNode(
            nums[mid_node], 
            self.sortedArrayToBST(nums[:mid_node]), self.sortedArrayToBST(nums[mid_node + 1 :])
        ) 
Logic and Algorithm Explanation

This code defines a function sortedArrayToBST that takes a sorted array of integers nums as input and returns the root node of a balanced Binary Search Tree (BST).
Here's a breakdown of the logic and algorithm:

1. Base Case:

If the input array is empty (not total_nums), then there's no valid BST to build, so the function returns None.

2. Recursive Construction:

If the array is not empty, the function finds the middle element (mid_node) using integer division (//) to ensure proper handling of even-sized arrays.
This middle element will become the root of the BST.
The function then recursively calls itself twice:
Once with the subarray nums[:mid_node] (containing elements less than the root) to build the left subtree.
Once with the subarray nums[mid_node + 1 :] (containing elements greater than the root) to build the right subtree.

3. Building the Node:

The function creates a new TreeNode instance with the middle element (nums[mid_node]) as its value.
It assigns the left subtree created with the first recursive call to the left child of the new node.
Similarly, it assigns the right subtree created with the second recursive call to the right child of the new node.
Finally, the function returns the newly created root node of the BST.

Overall Algorithm:

Check if the array is empty. If yes, return None.
Find the middle element and use it as the root value.
Recursively build the left subtree with elements less than the root.
Recursively build the right subtree with elements greater than the root.
Create a new node with the root value and assign left and right subtrees.
Return the root node of the constructed BST.

Time Complexity:

This algorithm has a time complexity of O(n log n), where n is the length of the input array. This is because each recursive call processes a subarray of half the size until it reaches the base case.

Space Complexity:

The space complexity is O(log n) due to the call stack involved in the recursive calls.

**Easy 3**

Given an integer numRows, return the first numRows of Pascal's triangle.
In Pascal's triangle, each number is the sum of the two numbers directly above it as shown:

Solution:

class Solution:

    def generate(self, numRows: int) -> List[List[int]]:
        result = []
        if numRows == 0:
            return result

        first_row = [1]
        result.append(first_row)

        for i in range(1, numRows):
            prev_row = result[i - 1]
            current_row = [1]

            for j in range(1, i):
                current_row.append(prev_row[j - 1] + prev_row[j])

            current_row.append(1)
            result.append(current_row)

        return result

Explanation of Logic and Algorithm:

This code defines a function generate that takes an integer numRows as input and returns a list of lists containing the elements of Pascal's triangle. Here's a breakdown of the logic and algorithm:

1. Initialization:

An empty list result is initialized to store the rows of Pascal's triangle.
If numRows is 0, meaning no rows are required, the empty result is returned.

2. Building the First Row:

A list first_row with the single element 1 is created and appended to result as the first row of the triangle.

3. Iterating over Subsequent Rows:

A loop iterates from 1 to numRows (excluding 0) to generate each subsequent row.

4. Building the Current Row:

Inside the loop, a new list current_row is initialized.
Two nested loops are used to populate current_row:
The outer loop iterates from 1 to the current row index (excluding 0).
The inner loop iterates over all elements of the previous row (except the last element).
Inside the nested loops, the value at each position in the current row is calculated by adding the corresponding elements from the previous row:


current_row.append(prev_row[j - 1] + prev_row[j])

Finally, the value 1 is appended to current_row as the last element.

5. Adding the Current Row and Updating the Previous Row:

The completed current_row is appended to result.
Now, the previous row (prev_row) is updated to become the current row for the next iteration:


prev_row = current_row

6. Final Result:

After iterating over all rows, the result containing all rows of Pascal's triangle is returned.

Overall Algorithm:

Initialize an empty list result to store rows.
Create and add the first row with one element (1).
Iterate over the required number of rows (excluding 0).
Inside the loop:
Initialize a new list current_row.
Use nested loops to iterate over each element of the current row.
Calculate each element by adding corresponding elements from the previous row.
Add 1 to the end of the current row.
Append the complete current row to result.
Update prev_row to become the current row.
Return the result containing all rows of Pascal's triangle.

Time Complexity:

The time complexity of this algorithm is O(n^2), where n is the number of rows (numRows). This is because of the nested loops iterating over each element in each row.

Space Complexity:

The space complexity is also O(n^2). This is because the result list stores all the rows, each containing n elements.
