## **Medium 1**
Given a binary search tree (BST), find the lowest common ancestor (LCA) node of two given nodes in the BST.According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”

*Solution*
~~~
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        # define a function to traverse the tree and find the lowest common ancestor of two nodes
        def traverse(root, p, q):
            # base case: return None when the node is None
            if not root:
                return None
            # return the node itself when it's one of the target nodes
            if root == p or root == q:
                return root
            # recursively search the left and right subtrees
            left = traverse(root.left, p, q)
            right = traverse(root.right, p, q)
            # if both left and right subtrees return a valid node, the current node is the lowest common ancestor
            if left and right:
                return root
            # if only one subtree returns a valid node, return that node
            return left or right

        # call the traverse function to find the lowest common ancestor
        return traverse(root, p, q)


        # Find the lowest common ancestor
        lowest_common_ancestor = None
        for node in common_ancestors:
            if lowest_common_ancestor is None or node.val < lowest_common_ancestor.val:
                lowest_common_ancestor = node

        return lowest_common_ancestor
~~~

**Logic and Algorithm Explanation:**

This code defines a function lowestCommonAncestor that takes the root of a binary tree and two nodes p and q as input, and returns the lowest common ancestor (LCA) of those nodes within the tree.

1. Inner Function Definition:

A nested function traverse is defined to recursively explore the tree and identify the LCA.

2. Base Cases:

Within traverse, the function checks for null nodes and immediately returns None if encountered.
It also checks if the current node is either p or q, and if so, returns the node itself as the LCA (base case).

3. Recursive Exploration:

The function recursively calls itself on both the left and right subtrees, passing the current node, p and q as arguments.
This essentially searches for the existence of p and q in both subtrees.

4. Identifying LCA:

There are three possible outcomes from the recursive calls:
Both subtrees return a valid node: This implies that the current node is the LCA as it has both p and q as descendants.
Only one subtree returns a valid node: That node itself is the LCA.
Both subtrees return None: No common ancestor is found in this subtree.

5. Returning the LCA:

The traverse function ultimately returns either the identified LCA node or None if no common ancestor is found.

6. Main Function:

The lowestCommonAncestor function simply calls the traverse function with the root node, p and q as arguments.
The final result returned by traverse is the LCA of the two nodes.

Overall Algorithm:

The code leverages recursion to explore both branches of the tree simultaneously.
By checking the presence of p and q in both subtrees and returning the first common ancestor encountered, the function efficiently identifies the LCA.

Time Complexity:

The time complexity of this algorithm is O(n), where n is the number of nodes in the tree. This is because each node is visited only once during the recursive exploration.

Space Complexity:

The space complexity is O(h), where h is the height of the tree. This is due to the call stack used during recursion, with the maximum depth being the height of the tree.

## **Medium 2**

Given an integer array of size n, find all elements that appear more than ⌊ n/3 ⌋ times.

*Solution:*
~~~
class Solution:
    def majorityElement(self, nums):
        return [num for num, count in Counter(nums).items() if count > len(nums) // 3]
~~~

**Logic and Algorithm Explanation:**

This code implements a concise approach to find the majority element(s) in a given list of integers. Here's a breakdown of the logic and algorithm:

1. Utilizing Collections.Counter:

The code uses the Counter class from the collections module. This built-in class efficiently counts the occurrences of each element in the input list nums.

2. Filtering by Frequency:

After creating the Counter object, the code iterates over its items. Each item in Counter is a tuple containing the element and its count (frequency). The code applies a conditional filter to keep only those elements whose count is greater than the threshold: count > len(nums) // 3.

3. Threshold Explanation:

The threshold len(nums) // 3 represents the minimum number of occurrences required for an element to be considered a majority element. This is because a majority element must appear more than half the time, which is equivalent to exceeding one-third of the elements in the list.

4. List Comprehension:

The filtered elements, which meet the frequency requirement, are extracted and converted into a list using list comprehension. This results in a list containing all the identified majority elements in the original nums list.

Overall Algorithm:

Use collections.Counter to count the occurrences of each element in the input list.
Iterate over the counter items and filter based on the frequency threshold.
Convert the filtered elements into a list using list comprehension.
Return the list of identified majority elements.

Time Complexity:

The time complexity of this algorithm is O(n), where n is the length of the input list. This is because both Counter and the list comprehension have linear time complexities.

Space Complexity:

The space complexity is also O(n). This includes the space required by the Counter object and the resulting list of majority elements.
