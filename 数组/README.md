[TOC]
# 167. 两数之和 II - 输入有序数组
## 题目
给定一个已按照升序排列 的有序数组，找到两个数使得它们相加之和等于目标数。
函数应该返回这两个下标值 index1 和 index2，其中 index1 必须小于 index2。
说明:
返回的下标值（index1 和 index2）不是从零开始的。
你可以假设每个输入只对应唯一的答案，而且你不可以重复使用相同的元素。
示例:
输入: numbers = [2, 7, 11, 15], target = 9
输出: [1,2]
解释: 2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 。  

## 参考文章

- [LeetCode\] Two Sum II - Input array is sorted 两数之和之二 - 输入数组有序](https://www.cnblogs.com/grandyang/p/5185815.html)

***
## 题解

### 我的题解

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        int size = numbers.size();
        if (size == 0 || size == 1) {
            return {};
        }
        int left = 0, right = size - 1;
        int sum = numbers[left] + numbers[right];
        while (sum != target) {
            while (sum < target) {
                left++;
                sum = numbers[left] + numbers[right];
            }
            while (sum > target) {
                right--;
                sum = numbers[left] + numbers[right];
            }
        }
        return {left + 1, right + 1};
    }
};
```

***
### 参考题解
```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        int size = numbers.size();
        if (size == 0 || size == 1) {
            return {};
        }
        int left = 0, right = size - 1;
        int sum = numbers[left] + numbers[right];
        while (sum != target) {
            while (sum < target) {
                left++;
                sum = numbers[left] + numbers[right];
            }
            while (sum > target) {
                right--;
                sum = numbers[left] + numbers[right];
            }
        }
        return {left + 1, right + 1};
    }
};
```
## 反思
easy

# 216. 组合总和 III

## 题目

找出所有相加之和为 n 的 k 个数的组合。组合中只允许含有 1 - 9 的正整数，并且每种组合中不存在重复的数字。

说明：

所有数字都是正整数。
解集不能包含重复的组合。 
示例 1:

输入: k = 3, n = 7
输出: [[1,2,4]]
示例 2:

输入: k = 3, n = 9
输出: [[1,2,6], [1,3,5], [2,3,4]]

## 参考文章

- [LeetCode\] Combination Sum III 组合之和之三](https://www.cnblogs.com/grandyang/p/4537983.html)
***
## 题解
### 我的题解

```c++
class Solution {
public:
    void DFS(vector<vector<int>> &res, int target, int start, vector<int> out, int num) {
        if (target == 0 && num == 0) {
            res.push_back(out);
            return;
        }
        if (target < 0 || num < 0) {
            return;
        }
        
        for (int i = start; i < 10; i++) {
            out.push_back(i);
            DFS(res, target - i, i + 1, out, num - 1);
            out.pop_back();
        }
    }
    
    vector<vector<int>> combinationSum3(int k, int n) {
        vector<vector<int>> res;
        if (k > 9) {
            return res;
        }
        DFS(res, n, 1, {}, k);
        return res;
    }
};
```

***
### 参考题解
```c++
class Solution {
public:
    vector<vector<int> > combinationSum3(int k, int n) {
        vector<vector<int> > res;
        vector<int> out;
        combinationSum3DFS(k, n, 1, out, res);
        return res;
    }
    void combinationSum3DFS(int k, int n, int level, vector<int> &out, vector<vector<int> > &res) {
        if (n < 0) return;
        if (n == 0 && out.size() == k) res.push_back(out);
        for (int i = level; i <= 9; ++i) {
            out.push_back(i);
            combinationSum3DFS(k, n - i, i + 1, out, res);
            out.pop_back();
        }
    }
};
```
## 反思
# 169. 求众数

## 题目
给定一个大小为 n 的数组，找到其中的众数。众数是指在数组中出现次数大于 ⌊ n/2 ⌋ 的元素。

你可以假设数组是非空的，并且给定的数组总是存在众数。

示例 1:

输入: [3,2,3]
输出: 3
示例 2:

输入: [2,2,1,1,1,2,2]
输出: 2
## 参考文章
- [[LeetCode] Majority Element 求大多数
](https://www.cnblogs.com/grandyang/p/4233501.html)
***
## 题解
### 我的题解
```c++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        if (nums.empty()) {
            return -1;
        }
        sort(nums.begin(), nums.end());
        int length = nums.size();
        int left = 0, right = length - 1;
        int mid = left + (right - left) / 2;
        return nums[mid];
    }
};
```

***
### 参考题解
```c++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int res = 0, cnt = 0;
        for (int num : nums) {
            if (cnt == 0) {res = num; ++cnt;}
            else (num == res) ? ++cnt : --cnt;
        }
        return res;
    }
};

class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int res = 0, n = nums.size();
        for (int i = 0; i < 32; ++i) {
            int ones = 0, zeros = 0;
            for (int num : nums) {
                if (ones > n / 2 || zeros > n / 2) break;
                if ((num & (1 << i)) != 0) ++ones;
                else ++zeros;
            }
            if (ones > zeros) res |= (1 << i);
        }
        return res;
    }
};
```
## 反思

- 摩尔投票法，实用计数器处理
- 我的做法只要O1就行了，竟然只超过一半的人，剩下都是什么玩意
- 位操作有点东西
# 229. 求众数 II
## 题目
给定一个大小为 n 的数组，找出其中所有出现超过 ⌊ n/3 ⌋ 次的元素。

说明: 要求算法的时间复杂度为 O(n)，空间复杂度为 O(1)。

示例 1:

输入: [3,2,3]
输出: [3]
示例 2:

输入: [1,1,1,3,3,2,2,2]
输出: [1,2]
## 参考文章

- [[LeetCode\] Majority Element II 求大多数之二](https://www.cnblogs.com/grandyang/p/4606822.html)
***
## 题解
### 我的题解
```c++
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
        if (nums.empty()) {
            return {};
        }
        if (nums.size() == 1) {
            return {nums[0]};
        }
        vector<int> res;
        int n = nums.size();
        int m = n / 3;
        int num = nums[0], count = 1;
        sort(nums.begin(), nums.end());
        nums.push_back(-1000);
        for (int i = 1; i < n + 1; i++) {
            if (nums[i] == nums[i - 1]) {
                count++;
            } else {
                if (count >= m) {
                    res.push_back(num);
                }
                num = nums[i];
                count = 1;
            }
        }
        return res;
    }
};
```

***
### 参考题解
```c++
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
        vector<int> res;
        int a = 0, b = 0, cnt1 = 0, cnt2 = 0, n = nums.size();
        for (int num : nums) {
            if (num == a) ++cnt1;
            else if (num == b) ++cnt2;
            else if (cnt1 == 0) { a = num; cnt1 = 1; }
            else if (cnt2 == 0) { b = num; cnt2 = 1; }
            else { --cnt1; --cnt2; }
        }
        cnt1 = cnt2 = 0;
        for (int num : nums) {
            if (num == a) ++cnt1;
            else if (num == b) ++cnt2;
        }
        if (cnt1 > n / 3) res.push_back(a);
        if (cnt2 > n / 3) res.push_back(b);
        return res;
    }
};
```
## 反思
- 佛了，还是数学问题呀，大于三分之一的最多有两个还行
# 189. 旋转数组
## 题目

给定一个数组，将数组中的元素向右移动 k 个位置，其中 k 是非负数。

示例 1:

输入: [1,2,3,4,5,6,7] 和 k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右旋转 1 步: [7,1,2,3,4,5,6]
向右旋转 2 步: [6,7,1,2,3,4,5]
向右旋转 3 步: [5,6,7,1,2,3,4]
示例 2:

输入: [-1,-100,3,99] 和 k = 2
输出: [3,99,-1,-100]
解释: 
向右旋转 1 步: [99,-1,-100,3]
向右旋转 2 步: [3,99,-1,-100]
说明:

尽可能想出更多的解决方案，至少有三种不同的方法可以解决这个问题。
要求使用空间复杂度为 O(1) 的 原地 算法。

## 参考文章
- [[LeetCode] 189. Rotate Array 旋转数组](https://www.cnblogs.com/grandyang/p/4298711.html)
***
## 题解
### 我的题解
```c++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int len = nums.size();
        if (len == 0 || (K %= len) == 0 || len == 1) {
            return;
        }
        int t = len;
        int start = 0, idx = 0, pre = 0, cur = nums[0];
        while (t--) {
            //pre：准备进行赋值的数据的数据
            //idx：下一个被赋值的下标
            //cur：保存idx上的原数据，也是下一个pre
            //strat：防止死循环
            pre = cur;
            idx = (idx + k) % n;
            cur = nums[idx];
            nums[idx] = pre;
            if (idx == start) {
                idx == ++start;
                cur = nums[idx];
            }
        }
        return;
    }
};
```

***
### 参考题解
```c++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        if (nums.empty()) return;
        int n = nums.size(), start = 0;   
        while (n && (k %= n)) {
            for (int i = 0; i < k; ++i) {
                swap(nums[i + start], nums[n - k + i + start]);
            }
            n -= k;
            start += k;
        }
    }
};

class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        if (nums.empty() || (k %= nums.size()) == 0) return;
        int n = nums.size();
        for (int i = 0; i < n - k; ++i) {
            nums.push_back(nums[0]);
            nums.erase(nums.begin());
        }
    }
};

class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        if (nums.empty() || (k %= nums.size()) == 0) return;
        int n = nums.size();
        reverse(nums.begin(), nums.begin() + n - k);
        reverse(nums.begin() + n - k, nums.end());
        reverse(nums.begin(), nums.end());
    }
};
```
## 反思
- 巨菜

# 228. 汇总区间

## 题目

给定一个无重复元素的有序整数数组，返回数组区间范围的汇总。

示例 1:

输入: [0,1,2,4,5,7]
输出: ["0->2","4->5","7"]
解释: 0,1,2 可组成一个连续的区间; 4,5 可组成一个连续的区间。
示例 2:

输入: [0,2,3,4,6,8,9]
输出: ["0","2->4","6","8->9"]
解释: 2,3,4 可组成一个连续的区间; 8,9 可组成一个连续的区间。

## 参考文章
- [LeetCode\] Summary Ranges 总结区间](https://www.cnblogs.com/grandyang/p/4603555.html)
***
## 题解
### 我的题解
```c++
class Solution {
public:
    vector<string> summaryRanges(vector<int>& nums) {
        vector<string> res;
        int i = 0, n = nums.size();
        while (i < n) {
          //i是当前区间的开头下标
            int j = 1; //j负责记录当前区间长度
            while (i + j < n && (long)nums[i + j] - nums[i] == j) ++j; //++j获取真正长度
            res.push_back(j == 1 ? to_string(nums[i]) : to_string(nums[i]) + "->" + to_string(nums[i + j - 1]));
          //分情况压入
          //to_string转字符串
            i += j;
        }
        return res;
    }
};
```

***
### 参考题解
```c++
class Solution {
public:
    vector<string> summaryRanges(vector<int>& nums) {
        if (nums.empty()) return {};
        vector<string> res;
        int l = nums[0], last = nums[0];
        for (int i = 1; i < nums.size(); ++i) {
            if (nums[i] != last + 1)
            {
                if (l == last) res.push_back(to_string(l));
                else res.push_back(to_string(l) + "->" + to_string(last));
                l = nums[i]; last = l;
            }
            else
                last = nums[i];
        }
        if (l == last) res.push_back(to_string(l));
        else res.push_back(to_string(l) + "->" + to_string(last));
        return res;
    }
};
```
## 反思

- 和to_string比，OC真的弟弟

# 217. 存在重复元素

## 题目

给定一个整数数组，判断是否存在重复元素。

如果任何值在数组中出现至少两次，函数返回 true。如果数组中每个元素都不相同，则返回 false。

示例 1:

输入: [1,2,3,1]
输出: true
示例 2:

输入: [1,2,3,4]
输出: false
示例 3:

输入: [1,1,1,3,3,4,3,2,4,2]
输出: true

## 参考文章
- [LeetCode\] Contains Duplicate 包含重复值](https://www.cnblogs.com/grandyang/p/4537029.html)
***
## 题解
### 我的题解
```c++
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        int len = nums.size();
        if (len == 0 || len == 1) {
            return false;
        }
        sort(nums.begin(), nums.end());
        for (int i = 0; i < len - 1; i++) {
            if (nums[i] == nums[i + 1]) {
                return true;
            }
        }
        return false;
    }
};
```

***
### 参考题解
```c++
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_map<int, int> m;
        for (int i = 0; i < nums.size(); ++i) {
            if (m.find(nums[i]) != m.end()) return true;
            ++m[nums[i]];
        }
        return false;
    }
};
```
## 反思

- find：在容器中搜索键值等于 k 的元素，如果找到，则返回一个指向该元素的迭代器，否则返回一个指向unordered_map :: end的迭代器。
- 使用方括号（[]），如果 k 匹配容器中某个元素的键，则该函数返回该映射值的引用，如果 k 与容器中任何元素的键都不匹配，则该函数将使用该键插入一个新元素，并返回该映射值的引用。
- ++m[]

# 219. 存在重复元素 II

## 题目

给定一个整数数组和一个整数 k，判断数组中是否存在两个不同的索引 i 和 j，使得 nums [i] = nums [j]，并且 i 和 j 的差的绝对值最大为 k。

示例 1:

输入: nums = [1,2,3,1], k = 3
输出: true
示例 2:

输入: nums = [1,0,1,1], k = 1
输出: true
示例 3:

输入: nums = [1,2,3,1,2,3], k = 2
输出: false

## 参考文章

- [219. 存在重复元素 II](https://leetcode-cn.com/problems/contains-duplicate-ii/)
***
## 题解

### 我的题解
```c++
class Solution {
public:
    bool containsNearbyDuplicate(vector<int>& nums, int k) {
        int len = nums.size();
        if (len == 0 || len == 1)  {
            return false;
        }
        for (int i = 0; i < k; i++) {
            nums.push_back(INT_MAX);
        }
        for (int i = 0; i < len; i++) {
            for (int j = i + 1; j <= i + k; j++) {
                if (nums[i] == nums[j]) {
                    return true;
                }
            }
        }
        return false;
    }
};
```

***
### 参考题解
```c++
class Solution {
public:
    bool containsNearbyDuplicate(vector<int>& nums, int k) {
        unordered_map<int, int> m;
        for (int i = 0; i < nums.size(); ++i) {
            if (m.find(nums[i]) != m.end() && i - m[nums[i]] <= k) 					return true;
            else m[nums[i]] = i;
        }
        return false;
    }
};
```
## 反思

- 我的想法就直白，就是跟着题目走，这里的问题在于遍历的重点，但是由于k困难会大于剩余值，极端情况就是数组长度只有3，k有4，导致无法用k去确定遍历范围
- 我的解决方法就是在数组里压了几个用不到的数据，这样就不用使用到临时变量计算k的范围了
- 但是倒数第二个测试数据多的压批，直接超时了
- 淦！这不就逼着用map吗，真的弟弟行为，这个map感觉要研究下，中午不做题目了，思考下

# 268. 缺失数字

## 题目

给定一个包含 0, 1, 2, ..., n 中 n 个数的序列，找出 0 .. n 中没有出现在序列中的那个数。

示例 1:

输入: [3,0,1]
输出: 2
示例 2:

输入: [9,6,4,2,3,5,7,0,1]
输出: 8
说明:
你的算法应具有线性时间复杂度。你能否仅使用额外常数空间来实现?

## 参考文章
- [LeetCode\] Missing Number 丢失的数字](https://www.cnblogs.com/grandyang/p/4756677.html)
***
## 题解
### 我的题解
```c++
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int res = 0;
        for (int i = 0; i < nums.size(); ++i) {
            res ^= (i + 1) ^ nums[i];
        }
        return res;
    }
};
```

***
### 参考题解
```c++
//位操作
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int res = 0;
        for (int i = 0; i < nums.size(); ++i) {
            res ^= (i + 1) ^ nums[i];
        }
        return res;
    }
};

//数组如果已经排过序 使用二分搜索
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int left = 0, right = nums.size();
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] > mid) right = mid;
            else left = mid + 1;
        }
        return right;
    }
};
```
## 反思

- 位操作好神秘啊
- 爷懂了，我们^的东西其实就是两份的数组，此外还有res这个0
- 0 ^ 4 = 4
- 4 ^ 4 = 0

# 238. 除自身以外数组的乘积

## 题目

给定长度为 n 的整数数组 nums，其中 n > 1，返回输出数组 output ，其中 output[i] 等于 nums 中除 nums[i] 之外其余各元素的乘积。

示例:

输入: [1,2,3,4]
输出: [24,12,8,6]
说明: 请不要使用除法，且在 O(n) 时间复杂度内完成此题。

进阶：
你可以在常数空间复杂度内完成这个题目吗？（ 出于对空间复杂度分析的目的，输出数组不被视为额外空间。）

## 参考文章

- [LeetCode\] 238. Product of Array Except Self 除本身之外的数组之积](https://www.cnblogs.com/grandyang/p/4650187.html)
***
## 题解
### 我的题解
```c++
//想不通呀
//我想的是用类似于前面做的数组偏移那样，把数组偏移n - 1，每次偏移都做乘法
//但这个时间复杂度得n平方
```

***
### 参考题解
```c++
//两个辅助数组
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        vector<int> fwd(n, 1), bwd(n, 1), res(n);
        for (int i = 0; i < n - 1; ++i) {
            fwd[i + 1] = fwd[i] * nums[i];
        }
        for (int i = n - 1; i > 0; --i) {
            bwd[i - 1] = bwd[i] * nums[i];
        }
        for (int i = 0; i < n; ++i) {
            res[i] = fwd[i] * bwd[i];
        }
        return res;
    }
};

//一个res数组搞定
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        vector<int> res(nums.size(), 1);
        for (int i = 1; i < nums.size(); ++i) {
            res[i] = res[i - 1] * nums[i - 1];
        }
        int right = 1;
        for (int i = nums.size() - 1; i >= 0; --i) {
            res[i] *= right;
            right *= nums[i];
        }
        return res;
    }
};
```
## 反思

- 没有想到是要分成两部分，两个部分乘起来

# 283. 移动零

## 题目

给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。

示例:

输入: [0,1,0,3,12]
输出: [1,3,12,0,0]
说明:

必须在原数组上操作，不能拷贝额外的数组。
尽量减少操作次数。

## 参考文章

- [LeetCode\] Move Zeroes 移动零](https://www.cnblogs.com/grandyang/p/4822732.html)
***
## 题解
### 我的题解
```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int len = nums.size();
        if (len == 0 || len == 1) {
            return;
        }
        int count = 0;
        for (int i = 0; i < len; i++) {
            if (nums[i] == 0) {
                count++;
            }
        }
        if (count == 0 || count == len) {
            return;
        }
        int cur = 0;
        for (int i = 0; i < len; i++) {
            if (cur >= len) {
                return;
            }
            while (cur < len && nums[cur] == 0) {
                cur++;    
            }
            if (cur >= len) {
                return;
            }
            swap(nums[i], nums[cur]);
            cur++;
            
        }
        return;
    }
};
```

***
### 参考题解
```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        for (int i = 0, j = 0; i < nums.size(); ++i) {
            if (nums[i]) {
                swap(nums[i], nums[j++]);
            }
        }
    }
};
```
## 反思

- 这里要注意，像while (cur < len && nums[cur] == 0)这样的判断必须把cur < len写在前面，不然会导致数组越界
- 大神是真的大神，这代码，我湿了
- i是后指针，j是前指针

# 287. 寻找重复数

## 题目

给定一个包含 n + 1 个整数的数组 nums，其数字都在 1 到 n 之间（包括 1 和 n），可知至少存在一个重复的整数。假设只有一个重复的整数，找出这个重复的数。

示例 1:

输入: [1,3,4,2,2]
输出: 2
示例 2:

输入: [3,1,3,4,2]
输出: 3
说明：

不能更改原数组（假设数组是只读的）。
只能使用额外的 O(1) 的空间。
时间复杂度小于 O(n2) 。
数组中只有一个重复的数字，但它可能不止重复出现一次。

## 参考文章
- [LeetCode\] Find the Duplicate Number 寻找重复数](https://www.cnblogs.com/grandyang/p/4843654.html)
***
## 题解

### 我的题解
```c++
//爷不会
//爷只会n平方解法 😢
```

***
### 参考题解
```c++
//二分
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int left = 0, right = nums.size();
        while (left < right){
            int mid = left + (right - left) / 2, cnt = 0;
            for (int num : nums) {
                if (num <= mid) ++cnt;
            }
            if (cnt <= mid) left = mid + 1;
            else right = mid;
        }    
        return right;
    }
};

//快慢指针环
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int slow = 0, fast = 0, t = 0;
        while (true) {
            slow = nums[slow];
            fast = nums[nums[fast]];
            if (slow == fast) break;
        }
        while (true) {
            slow = nums[slow];
            t = nums[t];
            if (slow == t) break;
        }
        return slow;
    }
};

//位操作
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int res = 0, n = nums.size();
        for (int i = 0; i < 32; ++i) {
            int bit = (1 << i), cnt1 = 0, cnt2 = 0;
            for (int k = 0; k < n; ++k) {
                if ((k & bit) > 0) ++cnt1;
                if ((nums[k] & bit) > 0) ++cnt2;
            }
            if (cnt2 > cnt1) res += bit;
        }
        return res;
    }
};
```
## 反思

- 只有二分能理解下。。。
- 明天不做题了，thinkthink

# 414. 第三大的数

## 题目

给定一个非空数组，返回此数组中第三大的数。如果不存在，则返回数组中最大的数。要求算法时间复杂度必须是O(n)。

示例 1:

输入: [3, 2, 1]

输出: 1

解释: 第三大的数是 1.
示例 2:

输入: [1, 2]

输出: 2

解释: 第三大的数不存在, 所以返回最大的数 2 .
示例 3:

输入: [2, 2, 3, 1]

输出: 1

解释: 注意，要求返回第三大的数，是指第三大且唯一出现的数。
存在两个值为2的数，它们都排第二。

## 参考文章
- [LeetCode\] Third Maximum Number 第三大的数](https://www.cnblogs.com/grandyang/p/5983113.html)
***
## 题解
### 我的题解
```c++
class Solution {
public:
    int thirdMax(vector<int>& nums) {
        int cur = INT_MIN, pre = INT_MIN, res = 0;
        int j = 2;
        bool flag = true;
        for (int &i : nums) {
            pre = max(i, pre);
        }
        res = pre;
        while (j--) {
            flag = true;
            cur = INT_MIN;
            for (int &i : nums) {
                if (i < pre) {
                    cur = max(i, cur);
                    flag = false;
                }
            }
            if (flag) {
                if (j >= 0) {
                    return res;
                }
                return pre;
            }
            pre = cur;
        }
        return cur;
    }
};
```

***
### 参考题解
```c++
//没爷的好
class Solution {
public:
    int thirdMax(vector<int>& nums) {
        long first = LONG_MIN, second = LONG_MIN, third = LONG_MIN;
        for (int num : nums) {
            if (num > first) {
                third = second;
                second = first;
                first = num;
            } else if (num > second && num < first) {
                third = second;
                second = num;
            } else if (num > third && num < second) {
                third = num;
            }
        }
        return (third == LONG_MIN || third == second) ? first : third;
    }
};

//set自动排序，去重
class Solution {
public:
    int thirdMax(vector<int>& nums) {
        set<int> s;
        for (int num : nums) {
            s.insert(num);
            if (s.size() > 3) {
                s.erase(s.begin());
            }
        }
        return s.size() == 3 ? *s.begin() : *s.rbegin();
    }
};
```
## 反思

- 不严谨，很多特殊情况没想到，以后做题一定要多思考，这leetcode是真的骚，INT_MIN都有，能给条活路不
- set有点东西的

# 442. 数组中的重复的数

## 题目

给定一个整数数组 a，其中1 ≤ a[i] ≤ n （n为数组长度）, 其中有些元素出现两次而其他元素出现一次。

找到所有出现两次的元素。

你可以不用到任何额外空间并在O(n)时间复杂度内解决这个问题吗？

示例：

输入:
[4,3,2,7,8,2,3,1]

输出:
[2,3]

## 参考文章
- [LeetCode\] Find All Duplicates in an Array 找出数组中所有重复项](https://www.cnblogs.com/grandyang/p/6209746.html)
***
## 题解
### 我的题解
```c++
class Solution {
public:
    vector<int> findDuplicates(vector<int>& nums) {
        int len = nums.size();
        int end = 0;
        vector<int> res(len, 0);
        for (int i = 0; i < len; i++) {
            res[nums[i] - 1]++;
            end = nums[i] - 1;
        }
        int j = 0;
        for (int i = 0; i < len; i++) {
            if (res[i] > 1) {
                res[j++] = i + 1;
            }
        }
        res.erase(res.begin() + j, res.end());
        return res;
    }
};
```

***
### 参考题解
```c++
//
class Solution {
public:
    vector<int> findDuplicates(vector<int>& nums) {
        vector<int> res;
        for (int i = 0; i < nums.size(); ++i) {
            int idx = abs(nums[i]) - 1;
            if (nums[idx] < 0) res.push_back(idx + 1);
            nums[idx] = -nums[idx];
        }
        return res;
    }
};

//
class Solution {
public:
    vector<int> findDuplicates(vector<int>& nums) {
        vector<int> res;
        for (int i = 0; i < nums.size(); ++i) {
            if (nums[i] != nums[nums[i] - 1]) {
                swap(nums[i], nums[nums[i] - 1]);
                --i;
            }
        }
        for (int i = 0; i < nums.size(); ++i) {
            if (nums[i] != i + 1) res.push_back(nums[i]);
        }
        return res;
    }
};

//
class Solution {
public:
    vector<int> findDuplicates(vector<int>& nums) {
        vector<int> res;
        int n = nums.size();
        for (int i = 0; i < n; ++i) {
            nums[(nums[i] - 1) % n] += n;
        }
        for (int i = 0; i < n; ++i) {
            if (nums[i] > 2 * n) res.push_back(i + 1);
        }
        return res;
    }
};
```
## 反思

- 明天见

# 1122. 数组的相对排序

## 题目

给你两个数组，arr1 和 arr2，

arr2 中的元素各不相同
arr2 中的每个元素都出现在 arr1 中
对 arr1 中的元素进行排序，使 arr1 中项的相对顺序和 arr2 中的相对顺序相同。未在 arr2 中出现过的元素需要按照升序放在 arr1 的末尾。

 

示例：

输入：arr1 = [2,3,1,3,2,4,6,7,9,2,19], arr2 = [2,1,4,3,9,6]
输出：[2,2,2,1,4,3,3,9,6,7,19]


提示：

arr1.length, arr2.length <= 1000
0 <= arr1[i], arr2[i] <= 1000
arr2 中的元素 arr2[i] 各不相同
arr2 中的每个元素 arr2[i] 都出现在 arr1 中

## 参考文章
- []()
***
## 题解
### 我的题解
```c++
class Solution {
public:
    vector<int> relativeSortArray(vector<int>& arr1, vector<int>& arr2) {
        
        int len1 = arr1.size(), len2 = arr2.size();
        
        if (len1 == 0) {
            return {};
        }
        vector<int> res;
        vector<int> buckets (1001, 0);
        int len3 = buckets.size();
        for (int &i : arr1) {
            buckets[i]++;
        }
        for (int &i : arr2) {
            while (buckets[i]--) {
                res.push_back(i);
            }
        }
        for (int i = 0; i < len3; i++) {
            if (buckets[i] > 0) {
                while (buckets[i]--) {
                    res.push_back(i);
                }
            }
        }
        return res;
    }
};
```

***
### 参考题解

```c++
//么得必要，我的题解写的够好了
```
## 反思

- 我的做法先给arr1整个桶排序，接着遍历arr2来作为buckets的下标进行排序，达到相对顺序的目的，同时要修改桶中的value
- 遍历完继续遍历buckets，这样值为-1的数字说明已经被输入到res当中，只要输出就行【这样就有序了】

# 448. 找到所有数组中消失的数字

## 题目

给定一个范围在  1 ≤ a[i] ≤ n ( n = 数组大小 ) 的 整型数组，数组中的元素一些出现了两次，另一些只出现一次。

找到所有在 [1, n] 范围之间没有出现在数组中的数字。

您能在不使用额外空间且时间复杂度为O(n)的情况下完成这个任务吗? 你可以假定返回的数组不算在额外空间内。

示例:

输入:
[4,3,2,7,8,2,3,1]

输出:
[5,6]

## 参考文章

- [题解：index大法](https://leetcode-cn.com/problems/find-all-numbers-disappeared-in-an-array/solution/cyuan-shu-zu-cao-zuo-by-haydenmiao/)

------

## 题解

### 我的题解

```c++
//只有思路
//由于限制了时间复杂度，所以不能排序
//其实这个抽屉原理的题目也看了好几道了，我能想到的就是index关系和位操作
```

------

### 参考题解

```c++
//做法就是想到index是跑不了的，我们根据遍历的num去修改对应下标的值
//同时我们进行的操作是加上一个长度，因此只要每次都取余，就可以获得本来的值了，妙啊
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
        vector<int> res;
        if(nums.empty()) return nums;
        for(int i=0;i<nums.size();i++)
        {
            int index=(nums[i]-1)%nums.size();
            nums[index]+=nums.size();
        }
        for(int i=0;i<nums.size();i++)
        {
            if(nums[i]<=nums.size())
                res.push_back(i+1);
        }
        return res;
    }
};
```

## 反思

- 题解大神还是有一手的

# 5182. 删除一次得到子数组最大和

## 题目

给你一个整数数组，返回它的某个 **非空** 子数组（连续元素）在执行一次可选的删除操作后，所能得到的最大元素总和。

换句话说，你可以从原数组中选出一个子数组，并可以决定要不要从中删除一个元素（只能删一次哦），（删除后）子数组中至少应当有一个元素，然后该子数组（剩下）的元素总和是所有子数组之中最大的。

注意，删除一个元素后，子数组 **不能为空**。

请看示例：

**示例 1：**

```
输入：arr = [1,-2,0,3]
输出：4
解释：我们可以选出 [1, -2, 0, 3]，然后删掉 -2，这样得到 [1, 0, 3]，和最大。
```

**示例 2：**

```
输入：arr = [1,-2,-2,3]
输出：3
解释：我们直接选出 [3]，这就是最大和。
```

**示例 3：**

```
输入：arr = [-1,-1,-1,-1]
输出：-1
解释：最后得到的子数组不能为空，所以我们不能选择 [-1] 并从中删去 -1 来得到 0。
     我们应该直接选择 [-1]，或者选择 [-1, -1] 再从中删去一个 -1。
```

 

**提示：**

- `1 <= arr.length <= 10^5`
- `-10^4 <= arr[i] <= 10^4`

## 参考文章

- [[Swift]LeetCode1185. 删除一次得到子数组最大和](https://www.cnblogs.com/strengthen/p/11484995.html)
***
## 题解
### 我的题解
```c++
class Solution {
public:
    void findMax (int start, vector<int>& arr, int &res) {
        int pre = 0;
        int k = 0;
        int n = arr.size();
        for (int i = start; i < n; i++) {
            if (arr[i] < 0) {
                if (arr[i] < k) {
                    pre += k;
                    k = arr[i];
                } else {
                    pre += arr[i];
                }
            } else {
                pre += arr[i];
            }
            res = max(res, pre);
            if (pre < 0) {
                pre = 0;
                k = 0;
                while (i < n && arr[i] <= 0) {
                    i++;
                }
                i--;
            }
        }
    }
    int maximumSum(vector<int>& arr) {
        int n = arr.size();
        if (n == 1) {
            return arr[0];  
        }
        int i = 0;
        int res = INT_MIN;
        while (i < n && arr[i] <= 0) {
            res = max(arr[i], res);
            i++;
        }
        if (i == n) {
            return res;
        }
        vector<int> nums;
        if (arr[0] > 0) {
            nums.push_back(0);
        }
        for (int j = 0; j < n - 1; j++) {
            if (arr[j + 1] > 0 && arr[j] <= 0) {
                nums.push_back(j + 1);
            }
        }
        for (int &p : nums) {
            findMax(p, arr, res);
        }
        // int pre = 0;
        // int k = 0;
        // // int k1 = 0;
        // for (; i < n; i++) {
        //     if (arr[i] < 0) {
        //         if (arr[i] < k) {
        //             pre += k;
        //             k = arr[i];
        //             k1 = i;
        //         } else {
        //             pre += arr[i];
        //             // if (pre < tmp) {
        //             //     pre = 0;
        //             //     k = 0;
        //             //     for (int &p : nums) {
        //             //         if (p > k1) {
        //             //             i = p - 1;
        //             //             break;
        //             //         }
        //             //     }
        //             // }
        //         }
        //     } else {
        //         pre += arr[i];
        //     }
        //     res = max(res, pre);
        //     if (pre < 0) {
        //         pre = 0;
        //         k = 0;
        //         while (i < n && arr[i] <= 0) {
        //             i++;
        //         }
        //         i--;
        //     }
        // }
        return res;
    }
};
```

***
### 参考题解
```c++
class Solution {
public:
    int maximumSum(vector<int>& arr) {
        int n = arr.size();
        if (n == 1) {
            return arr[0];
        }
        vector<int> leftMaxSum(n, 0);
        for (int i = 1; i < n; i++) {
            leftMaxSum[i] = max(arr[i - 1], leftMaxSum[i - 1] + arr[i - 1]);
          //这个遍历的意思是当前遍到的这一位视作忽略
          //也就是说对于leftMaxSum[1]就是视作把arr[0]忽略掉的从最左边开始的子数组
        }
        vector<int> rightMaxSum(n, 0);
        for (int i = n - 2; i > -1; i--) {
            rightMaxSum[i] = max(arr[i + 1], rightMaxSum[i + 1] + arr[i + 1]);
          //right同理，就是从右往左的一个子数组
        }
        int maxNum = max(leftMaxSum[n - 1], rightMaxSum[0]);
      	//初值
        for (int i = 1; i < n - 1; i++) {
            maxNum = max(maxNum, leftMaxSum[i]);
            maxNum = max(maxNum, rightMaxSum[i]);
            maxNum = max(maxNum, leftMaxSum[i] + rightMaxSum[i]);
          //这种情况就是中间舍弃了一个
        }
        return maxNum;
    }
};
```
## 反思

- 太菜
- 巨菜
- 好菜

# 215. 数组中的第K个最大元素

## 题目

在未排序的数组中找到第 k 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

示例 1:

输入: [3,2,1,5,6,4] 和 k = 2
输出: 5
示例 2:

输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4
说明:

你可以假设 k 总是有效的，且 1 ≤ k ≤ 数组的长度。

## 参考文章

- 8⃣️需要哦
***
## 题解
### 我的题解
```c++
class Solution {
public:
    int partition(vector<int> &nums, int p, int r) {
        
        if (p == r) {
            return p;
        }
        
        int pivot = nums[r];
        int i = p;
        for (int j = p; j < r; j++) {
            if (nums[j] > pivot) {
                swap(nums[i], nums[j]);
                i++;
            }
        }
        swap(nums[i], nums[r]);
        return i;
    }
    int findKthLargest(vector<int>& nums, int k) {
        
        int len = nums.size();
        if (len == 0 || len < k) {
            return 0;
        }
        int res = 0;
        int p = 0;
        int r = len;
        while (1) {
            int index = partition(nums, p, r - 1);
            // res += index;
            if ((index + 1) == k) {
                return nums[index];
            } else if ((index + 1) > k) {
                r = index;
            } else {
                p = index + 1;
            }
        }
        return -99;
    }
};
```

***
### 参考题解

- 8⃣️需要哦

## 反思

- 对于这个上边界还是有点问题

# 862. 和至少为K的最短子数组

## 题目

返回 A 的最短的非空连续子数组的长度，该子数组的和至少为 K 。

如果没有和至少为 K 的非空子数组，返回 -1 。

 

示例 1：

输入：A = [1], K = 1
输出：1
示例 2：

输入：A = [1,2], K = 4
输出：-1
示例 3：

输入：A = [2,-1,2], K = 3
输出：3


提示：

1 <= A.length <= 50000
-10 ^ 5 <= A[i] <= 10 ^ 5
1 <= K <= 10 ^ 9

## 参考文章
- [LeetCode\] 862. Shortest Subarray with Sum at Least K 和至少为K的最短子数组](https://www.cnblogs.com/grandyang/p/11300071.html)

***
## 题解
### 我的题解

```c++
#include <iostream>
#include <vector>
#include <deque>

using namespace std;

class Solution {
public:
	int shortestSubarray(vector<int>& A, int K) {
		int n = A.size(), res = INT_MAX;
		deque<int> dq;
		vector<int> sums(n + 1);
		for (int i = 1; i <= n; ++i) sums[i] = sums[i - 1] + A[i - 1];
		//打印nums的内容
		for (int i = 0; i < sums.size(); i++) {
			cout << "sums[" << i << "] :"  << sums[i] << '\t';
		}
		cout << "\n";
		for (int i = 0; i <= n; ++i) {
			cout << "当前的i是:" << i << endl;
			cout << "NO1 打印DP START:" << endl;
			//打印deque的内容
			for (int i = 0; i < dq.size(); i++) {
				cout << "dq[" << i << "] :"  << dq[i] << '\t';
			}
			cout << "\n";
			cout << "NO1 打印DP END:" << endl;

			while (!dq.empty() && sums[i] - sums[dq.front()] >= K) {
				cout << "NO2 打印DP START:" << endl;
				//打印deque的内容
				for (int i = 0; i < dq.size(); i++) {
					cout << "dq[" << i << "] :"  << dq[i] << '\t';
				}
				cout << "\n";
				cout << "NO2 打印DP END:" << endl;
				cout << "OLD res:" << res << endl;
				res = min(res, i - dq.front());
				cout << "NEW res:" << res << endl;
				dq.pop_front();
			}
			while (!dq.empty() && sums[i] <= sums[dq.back()]) {
				cout << "NO3 打印DP START:" << endl;
				//打印deque的内容
				for (int i = 0; i < dq.size(); i++) {
					cout << "dq[" << i << "] :"  << dq[i] << '\t';
				}
				cout << "\n";
				cout << "NO3 打印DP END:" << endl;
				dq.pop_back();
			}
			cout << "NO4 打印DP START:" << endl;
			//打印deque的内容
			for (int i = 0; i < dq.size(); i++) {
				cout << "dq[" << i << "] :"  << dq[i] << '\t';
			}
			cout << "\n";
			cout << "NO4 打印DP END:" << endl;
			dq.push_back(i);
		}
		return res == INT_MAX ? -1 : res;
	}
};
int main(int argc, char *argv[]) {
	Solution f;
	vector<int> arr = {168};
	int res = f.shortestSubarray(arr, 167);
	cout << res << endl;
}
```

***
### 参考题解

```c++
class Solution {
public:
    int shortestSubarray(vector<int>& A, int K) {
        int n = A.size(), res = INT_MAX;
        deque<int> dq;
        vector<int> sums(n + 1);
        for (int i = 1; i <= n; ++i) sums[i] = sums[i - 1] + A[i - 1];
        for (int i = 0; i <= n; ++i) {
            while (!dq.empty() && sums[i] - sums[dq.front()] >= K) {
                res = min(res, i - dq.front());
                dq.pop_front();
            }
            while (!dq.empty() && sums[i] <= sums[dq.back()]) {
                dq.pop_back();
            }
            dq.push_back(i);
        }
        return res == INT_MAX ? -1 : res;
    }
};
```
## 反思

- 大神的做法妙是真的妙，难懂也是真的难懂
- 可以看官方题解的解释[和至少为K的最短子数组](https://leetcode-cn.com/problems/shortest-subarray\-with-sum-at-least-k/solution/he-zhi-shao-wei-k-de-zui-duan-zi-shu-zu-by-leetcod/)
- 关键是要理解我们的队列里面存放的到底是什么，其实存放的是我们结果子数组的左首，遍历到的i才是右首，队列里要保证的是能放进去的，作为小于K的子数组

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