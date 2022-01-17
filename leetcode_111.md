## Leetcode: Minimum Depth of Binary Tree (111)
### Question

Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

Note: A leaf is a node with no children.

Example 1:

Input: root = [3,9,20,null,null,15,7]
Output: 2

Example 2:

Input: root = [2,null,3,null,4,null,5,null,6]
Output: 5
 

Constraints:

The number of nodes in the tree is in the range [0, 105].
-1000 <= Node.val <= 1000


#### Solution #1
In this solution, I used `Tree Recursion` to traverse the binary tree. The function will return the depth.

(1) If root != NULL
    - If root->left != NULL && root->right == NULL, return 1 + minDepth(root->left)
    - If root->right != NULL && root->left == NULL, return 1 + minDepth(root->right)
    - Else, return min(minDepth(root->left), minDepth(root->right))
(2) If root == NULL, return 0;

``` cpp
class Solution {
public:
    int minDepth(TreeNode* root) {
        if(root != NULL)
        {
            if(root->left == NULL && root->right != NULL)
            {
                return minDepth(root->right) + 1;
            }
            if(root->right == NULL && root->left != NULL)
            {
                return minDepth(root->left) + 1;
            }
            return std::min(minDepth(root->left), minDepth(root->right)) + 1;
        }
        return 0;
    }
};
```