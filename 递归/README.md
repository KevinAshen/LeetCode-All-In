[TOC]
# 622. 最长同值路径

## 题目

给定一个二叉树，找到最长的路径，这个路径中的每个节点具有相同值。 这条路径可以经过也可以不经过根节点。

注意：两个节点之间的路径长度由它们之间的边数表示。

示例 1:

输入:

              5
             / \
            4   5
           / \   \
          1   1   5
输出:

2
示例 2:

输入:

              1
             / \
            4   5
           / \   \
          4   4   5
输出:

2
注意: 给定的二叉树不超过10000个结点。 树的高度不超过1000。

## 参考文章
- [LeetCode官方题解](https://leetcode-cn.com/problems/longest-univalue-path/solution/zui-chang-tong-zhi-lu-jing-by-leetcode/)
***
## 题解
### 我的题解
```c++
// 这谁会啊
```

***
### 参考题解
```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int ans;
    int longestUnivaluePath(TreeNode* root) {
        ans = 0;
        arrowLength(root);
        return ans;
    }
    int arrowLength(TreeNode* node) {
        if (node == NULL) {
            return 0;
        }
        int left = arrowLength(node->left);
        int right = arrowLength(node->right);
        int arrowLeft = 0, arrowRight = 0;
        if (node->left != NULL && node->left->val == node->val) {
            arrowLeft += left + 1;
        }
        if (node->right != NULL && node->right->val == node->val) {
            arrowRight += right + 1;
        }
        ans = max(ans, arrowLeft + arrowRight);
        return max(arrowLeft, arrowRight);
    }
};
```
## 反思

- 一个问题的解可以分解为几个子问题的解
  - 首先对于树形结构，我们肯定是从根结点往下遍历，对于每个结点，我们的长度本质是对其在左结点以及右结点路径和上在+1
  - 当然还是很难懂，怪不得说递归是最难的了，虾米玩意
- 这个问题与分解之后的子问题，除了数据规模不同，求解思路完全一样
  - 这个在第一点也说明的很清楚了
- 存在递归终止条件
  - 这个很简单，对与树形结构，在碰到结点为NULL肯定终止了
- 好难，感觉自己做还是整不出来
- 只能理解下

# XXX. SSSS

## 题目
## 参考文章
- []()
***
## 题解
### 我的题解
```c++

```

***
### 参考题解
```c++

```
## 反思

# XXX. SSSS

## 题目
## 参考文章
- []()
***
## 题解
### 我的题解
```c++

```

***
### 参考题解
```c++

```
## 反思


# XXX. SSSS

## 题目
## 参考文章
- []()
***
## 题解
### 我的题解
```c++

```

***
### 参考题解
```c++

```
## 反思


# XXX. SSSS

## 题目
## 参考文章
- []()
***
## 题解
### 我的题解
```c++

```

***
### 参考题解
```c++

```
## 反思


# XXX. SSSS

## 题目
## 参考文章
- []()
***
## 题解
### 我的题解
```c++

```

***
### 参考题解
```c++

```
## 反思


# XXX. SSSS

## 题目
## 参考文章
- []()
***
## 题解
### 我的题解
```c++

```

***
### 参考题解
```c++

```
## 反思


# XXX. SSSS

## 题目
## 参考文章
- []()
***
## 题解
### 我的题解
```c++

```

***
### 参考题解
```c++

```
## 反思


# XXX. SSSS

## 题目
## 参考文章
- []()
***
## 题解
### 我的题解
```c++

```

***
### 参考题解
```c++

```
## 反思

# XXX. SSSS

## 题目
## 参考文章
- []()
***
## 题解
### 我的题解
```c++

```

***
### 参考题解
```c++

```
## 反思

# XXX. SSSS

## 题目
## 参考文章
- []()
***
## 题解
### 我的题解
```c++

```

***
### 参考题解
```c++

```
## 反思

# XXX. SSSS

## 题目
## 参考文章
- []()
***
## 题解
### 我的题解
```c++

```

***
### 参考题解
```c++

```
## 反思

# XXX. SSSS

## 题目
## 参考文章
- []()
***
## 题解
### 我的题解
```c++

```

***
### 参考题解
```c++

```
## 反思

# XXX. SSSS

## 题目
## 参考文章
- []()
***
## 题解
### 我的题解
```c++

```

***
### 参考题解
```c++

```
## 反思

# XXX. SSSS

## 题目
## 参考文章
- []()
***
## 题解
### 我的题解
```c++

```

***
### 参考题解
```c++

```
## 反思

# XXX. SSSS

## 题目
## 参考文章
- []()
***
## 题解
### 我的题解
```c++

```

***
### 参考题解
```c++

```
## 反思

# XXX. SSSS

## 题目
## 参考文章
- []()
***
## 题解
### 我的题解
```c++

```

***
### 参考题解
```c++

```
## 反思

# XXX. SSSS

## 题目
## 参考文章
- []()
***
## 题解
### 我的题解
```c++

```

***
### 参考题解
```c++

```
## 反思