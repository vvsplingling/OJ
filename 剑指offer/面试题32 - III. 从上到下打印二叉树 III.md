### [面试题32 - III. 从上到下打印二叉树 III](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)

两个栈

```c++
/**

 * Definition for a binary tree node.
 * struct TreeNode {
 * int val;
 * TreeNode *left;
 * TreeNode *right;
 * TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
   */
   class Solution {
   public:
   vector<vector<int>> levelOrder(TreeNode* root) {
       if(root==NULL)
           return {};
       vector<vector<int>> res;
       stack<TreeNode*> s1;
       stack<TreeNode*> s2;
       s1.push(root);
       for(;;){
           vector<int> tmp;
           while(!s1.empty()){
               tmp.push_back(s1.top()->val);
               if(s1.top()->left)
                   s2.push(s1.top()->left);
               if(s1.top()->right)
                   s2.push(s1.top()->right);
               s1.pop();
           }
           res.push_back(tmp);
           vector<int> temp;
           while(!s2.empty()){
               temp.push_back(s2.top()->val);
               if(s2.top()->right)
                   s1.push(s2.top()->right);
               if(s2.top()->left)
                   s1.push(s2.top()->left);
               s2.pop();
           }
           if(!temp.empty())
               res.push_back(temp);
           if(s1.empty()&&s2.empty())
               break;
       }
       return res;
   }
   };
```