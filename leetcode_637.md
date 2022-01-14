## Leetcode: Average of Levels in Binary Tree (637)
### Question

Given the root of a binary tree, return the average value of the nodes on each level in the form of an array. Answers within 10-5 of the actual answer will be accepted.
 

Example 1:

Input: root = [3,9,20,null,null,15,7]
Output: [3.00000,14.50000,11.00000]

Explanation: The average value of nodes on level 0 is 3, on level 1 is 14.5, and on level 2 is 11.
Hence return [3, 14.5, 11].

Example 2:

Input: root = [3,9,20,15,7]
Output: [3.00000,14.50000,11.00000]
 
Constraints:

The number of nodes in the tree is in the range [1, 104].
-231 <= Node.val <= 231 - 1

#### Solution #1
I used a queue to do a level-order traversal. In addition, I used the size of the queue to add a constraint of how many iteration the loop should do for each level. 

``` cpp
class Solution {
public:
    vector<double> averageOfLevels(TreeNode* root) {
        
        // result vector
        vector<double> r;
        
        // edge case
        if(root->left == NULL && root->right == NULL)
        {
            r.push_back(root->val);
            return r;
        }
        
        // declare queue and insert root node
        queue<TreeNode*> q;
        q.push(root);
        
        
        // loop until queue is empty
        while(!q.empty())
        {
            TreeNode* ptr = NULL;   // current node pointer
            int size = q.size();    // queue size
            double total = 0;
            
            // pop nodes from the queue n times (n = size)
            for(int i = 0; i < size; i++)
            {
                ptr = q.front();
                q.pop();
                
                // push child nodes into the queue if !NULL
                if(ptr->left != NULL)
                    q.push(ptr->left);
                if(ptr->right != NULL)
                    q.push(ptr->right);
                
                // add the current node val to total
                total += ptr->val;
            }
            // insert avg into result vector
            r.push_back(total/size);
        }
        
        
        return r;
        
    }
};
```
