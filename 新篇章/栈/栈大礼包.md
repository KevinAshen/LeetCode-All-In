[TOC]
# 20. 有效的括号

## 题目

给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
注意空字符串可被认为是有效字符串。

示例 1:

输入: "()"
输出: true
示例 2:

输入: "()[]{}"
输出: true
示例 3:

输入: "(]"
输出: false
示例 4:

输入: "([)]"
输出: false
示例 5:

输入: "{[]}"
输出: true

## 参考文章
- [LeetCode\] Valid Parentheses 验证括号](https://www.cnblogs.com/grandyang/p/4424587.html)
***
## 题解
### 我的题解
```c++
class Solution {
public:
    bool isValid(string s) {
        stack<char> parentheses;
        for (int i = 0; i < s.size(); i++) {
            if (s[i] == '(' || s[i] == '[' || s[i] == '{') {
                parentheses.push(s[i]);
            } else {
                if (parentheses.empty()) {
                    return false;
                }
                if (s[i] == ')' && parentheses.top() != '(') {
                    return false;
                }
                if (s[i] == ']' && parentheses.top() != '[') {
                    return false;
                }
                if (s[i] == '}' && parentheses.top() != '{') {
                    return false;
                }
                parentheses.pop();
            }
           
        }
         return parentheses.empty();
    }
};
```

***
### 参考题解
```c++
class Solution {
public:
    bool isValid(string s) {
        stack<char> parentheses;
        for (int i = 0; i < s.size(); ++i) {
            if (s[i] == '(' || s[i] == '[' || s[i] == '{') parentheses.push(s[i]);
            else {
                if (parentheses.empty()) return false;
                if (s[i] == ')' && parentheses.top() != '(') return false;
                if (s[i] == ']' && parentheses.top() != '[') return false;
                if (s[i] == '}' && parentheses.top() != '{') return false;
                parentheses.pop();
            }
        }
        return parentheses.empty();
    }
};
```
## 反思

- stack<int> a

# 155. 最小栈

## 题目

设计一个支持 push，pop，top 操作，并能在常数时间内检索到最小元素的栈。

push(x) -- 将元素 x 推入栈中。
pop() -- 删除栈顶的元素。
top() -- 获取栈顶元素。
getMin() -- 检索栈中的最小元素。
示例:

MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.getMin();   --> 返回 -2.

## 参考文章
- []()
***
## 题解
### 我的题解
```c++
class MinStack {
public:
    /** initialize your data structure here. */
    MinStack() {
        
    }
    
    void push(int x) {
        s1.push(x);
        if (s2.empty() || x <= s2.top()) {
            s2.push(x);
        }
    }
    
    void pop() {
        if (s1.top() == s2.top()) {
            s2.pop();
        }
        s1.pop();
    }
    
    int top() {
        return s1.top();
    }
    
    int getMin() {
        return s2.top();
    }

private:
    stack<int> s1, s2;

};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(x);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */
```

***
### 参考题解
```c++
class MinStack {
public:
    MinStack() {}    
    void push(int x) {
        s1.push(x);
        if (s2.empty() || x <= s2.top()) s2.push(x);
    }    
    void pop() {
        if (s1.top() == s2.top()) s2.pop();
        s1.pop();
    }  
    int top() {
        return s1.top();
    }    
    int getMin() {
        return s2.top();
    }
    
private:
    stack<int> s1, s2;
};
```
## 反思

- 这里要注意为什么只要把比s1栈顶小的元素压入s2就行了，问题在于由于栈只能从顶上一个个pop，这就导致，小的会一直在下面，直到上面的都被pop

# 232. 用栈实现队列

## 题目

使用栈实现队列的下列操作：

push(x) -- 将一个元素放入队列的尾部。
pop() -- 从队列首部移除元素。
peek() -- 返回队列首部的元素。
empty() -- 返回队列是否为空。
示例:

MyQueue queue = new MyQueue();

queue.push(1);
queue.push(2);  
queue.peek();  // 返回 1
queue.pop();   // 返回 1
queue.empty(); // 返回 false
说明:

你只能使用标准的栈操作 -- 也就是只有 push to top, peek/pop from top, size, 和 is empty 操作是合法的。
你所使用的语言也许不支持栈。你可以使用 list 或者 deque（双端队列）来模拟一个栈，只要是标准的栈操作即可。
假设所有操作都是有效的 （例如，一个空的队列不会调用 pop 或者 peek 操作）。

## 参考文章

- [LeetCode\] Implement Queue using Stacks 用栈来实现队列](https://www.cnblogs.com/grandyang/p/4626238.html)
***
## 题解
### 我的题解
```c++
class MyQueue {
public:
    /** Initialize your data structure here. */
    MyQueue() {
        
    }
    
    /** Push element x to the back of queue. */
    void push(int x) {
        stack<int> tmp;
        while (!st.empty()) {
            tmp.push(st.top());
            st.pop();
        }
        st.push(x);
        while (!tmp.empty()) {
            st.push(tmp.top());
            tmp.pop();
        }
    }
    
    /** Removes the element from in front of queue and returns that element. */
    int pop() {
        int val = st.top();
        st.pop();
        return val;
    }
    
    /** Get the front element. */
    int peek() {
        return st.top();
    }
    
    /** Returns whether the queue is empty. */
    bool empty() {
        return st.empty();   
    }

private:
    stack<int> st;
};

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue* obj = new MyQueue();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->peek();
 * bool param_4 = obj->empty();
 */
```

***
### 参考题解
```c++
class MyQueue {
public:
    /** Initialize your data structure here. */
    MyQueue() {}
    
    /** Push element x to the back of queue. */
    void push(int x) {
        _new.push(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    int pop() {
        shiftStack();
        int val = _old.top(); _old.pop();
        return val;
    }
    
    /** Get the front element. */
    int peek() {
        shiftStack();
        return _old.top();
    }
    
    /** Returns whether the queue is empty. */
    bool empty() {
        return _old.empty() && _new.empty();
    }
    
    void shiftStack() {
        if (!_old.empty()) return;
        while (!_new.empty()) {
            _old.push(_new.top());
            _new.pop();
        }
    }
    
private:
    stack<int> _old, _new;
};
```
## 反思

- 队列先进先出，栈先进后出

# 224. 基本计算器

## 题目

实现一个基本的计算器来计算一个简单的字符串表达式的值。

字符串表达式可以包含左括号 ( ，右括号 )，加号 + ，减号 -，非负整数和空格  。

示例 1:

输入: "1 + 1"
输出: 2
示例 2:

输入: " 2-1 + 2 "
输出: 3
示例 3:

输入: "(1+(4+5+2)-3)+(6+8)"
输出: 23
说明：

你可以假设所给定的表达式都是有效的。
请不要使用内置的库函数 eval。

## 参考文章
- [LeetCode\] Basic Calculator 基本计算器](https://www.cnblogs.com/grandyang/p/4570699.html)
***
## 题解
### 我的题解
```c++
class Solution {
public:
    int calculate(string s) {
        int res = 0, sign = 1, n = s.size();
        stack<int> st;
        for (int i = 0; i < n; ++i) {
            char c = s[i];
            if (c >= '0') {
                int num = 0;
                while (i < n && s[i] >= '0') {
                    num = 10 * num + (s[i++] - '0');
                }
                res += sign * num;
                --i;
            } else if (c == '+') {
                sign = 1;
            } else if (c == '-') {
                sign = -1;
            } else if (c == '(') {
                st.push(res);
                st.push(sign);
                res = 0;
                sign = 1;
            } else if (c == ')') {
                res *= st.top(); st.pop();
                res += st.top(); st.pop();
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
    int calculate(string s) {
        int res = 0, num = 0, sign = 1, n = s.size();
        stack<int> st;
        for (int i = 0; i < n; ++i) {
            char c = s[i];
            if (c >= '0') {
                num = 10 * num + (c - '0');
            } else if (c == '+' || c == '-') {
                res += sign * num;
                num = 0;
                sign = (c == '+') ? 1 : -1;
             } else if (c == '(') {
                st.push(res);
                st.push(sign);
                res = 0;
                sign = 1;
            } else if (c == ')') {
                res += sign * num;
                num = 0;
                res *= st.top(); st.pop();
                res += st.top(); st.pop();
            }
        }
        res += sign * num;
        return res;
    }
};
```
## 反思

- 要思考

# 682. 棒球比赛

## 题目

你现在是棒球比赛记录员。
给定一个字符串列表，每个字符串可以是以下四种类型之一：
1.整数（一轮的得分）：直接表示您在本轮中获得的积分数。
2. "+"（一轮的得分）：表示本轮获得的得分是前两轮有效 回合得分的总和。
3. "D"（一轮的得分）：表示本轮获得的得分是前一轮有效 回合得分的两倍。
4. "C"（一个操作，这不是一个回合的分数）：表示您获得的最后一个有效 回合的分数是无效的，应该被移除。

每一轮的操作都是永久性的，可能会对前一轮和后一轮产生影响。
你需要返回你在所有回合中得分的总和。

示例 1:

输入: ["5","2","C","D","+"]
输出: 30
解释: 
第1轮：你可以得到5分。总和是：5。
第2轮：你可以得到2分。总和是：7。
操作1：第2轮的数据无效。总和是：5。
第3轮：你可以得到10分（第2轮的数据已被删除）。总数是：15。
第4轮：你可以得到5 + 10 = 15分。总数是：30。
示例 2:

输入: ["5","-2","4","C","D","9","+","+"]
输出: 27
解释: 
第1轮：你可以得到5分。总和是：5。
第2轮：你可以得到-2分。总数是：3。
第3轮：你可以得到4分。总和是：7。
操作1：第3轮的数据无效。总数是：3。
第4轮：你可以得到-4分（第三轮的数据已被删除）。总和是：-1。
第5轮：你可以得到9分。总数是：8。
第6轮：你可以得到-4 + 9 = 5分。总数是13。
第7轮：你可以得到9 + 5 = 14分。总数是27。
注意：

输入列表的大小将介于1和1000之间。
列表中的每个整数都将介于-30000和30000之间。

## 参考文章
- [LeetCode官方题解下方评论区](https://leetcode-cn.com/problems/baseball-game/solution/bang-qiu-bi-sai-by-leetcode/)
***
## 题解

### 我的题解
```c++
class Solution {
public:
    int calPoints(vector<string>& ops) {
        int opsLen = ops.size();
        stack<int> numStack;
        
        for (int i = 0; i < opsLen; i++) {
            string tmpStr = ops[i];
            int tmpStrLen = ops[i].size();
            int tmpNum = 0;
            int sign = 1;
            //负数情况还没有考虑
            if ((tmpStr[0] >= '0' && tmpStr[0] <= '9') || tmpStr[0] == '-') {
                int j = 0;
                if (tmpStr[0] == '-') {
                    sign = -1;
                    j = 1;
                }
                for (; j < tmpStrLen; j++) {
                    tmpNum = 10 * tmpNum + (tmpStr[j] - '0');
                }
                //return tmpStrLen;
                numStack.push(tmpNum * sign);
            } else {
                if (tmpStr[0] == '+') {
                    int topNum = numStack.top();
                    numStack.pop();
                    tmpNum += numStack.top();
                    tmpNum += topNum;
                    numStack.push(topNum);
                    numStack.push(tmpNum);
                }
                if (tmpStr[0] == 'D') {
                    int topNum = numStack.top();
                    tmpNum += 2 * topNum;
                    numStack.push(tmpNum);
                }
                if (tmpStr[0] == 'C') {
                    numStack.pop();
                }
            }
        }
        
        int res = 0;
        while (!numStack.empty()) {
            res += numStack.top();
            numStack.pop();
        }
        return res;
    }
};
```

***
### 参考题解
```c++
int calPoints(vector<string>& ops) {
		stack<int>stack;
		for (string it : ops) {
			if (it == "+") {
				int top = stack.top(); stack.pop();
				int new_top = top + stack.top();
				stack.push(top);
				stack.push(new_top);
			}
			else if (it == "C") stack.pop();
			else if (it == "D") stack.push(2 * stack.top());
			else stack.push(atoi(it.c_str()));
		}
		int res = 0, n=stack.size();
		for (int i = 0; i < n; i++) {
			res += stack.top();
			stack.pop();
		}
		return res;
	}
```
## 反思

- 爷做了半天跟我说有string转数字的函数？💩
- atoi(it.c_str())【学就完事了】

# 496. 下一个更大元素 I

## 题目

给定两个没有重复元素的数组 nums1 和 nums2 ，其中nums1 是 nums2 的子集。找到 nums1 中每个元素在 nums2 中的下一个比其大的值。

nums1 中数字 x 的下一个更大元素是指 x 在 nums2 中对应位置的右边的第一个比 x 大的元素。如果不存在，对应位置输出-1。

示例 1:

输入: nums1 = [4,1,2], nums2 = [1,3,4,2].
输出: [-1,3,-1]
解释:
    对于num1中的数字4，你无法在第二个数组中找到下一个更大的数字，因此输出 -1。
    对于num1中的数字1，第二个数组中数字1右边的下一个较大数字是 3。
    对于num1中的数字2，第二个数组中没有下一个更大的数字，因此输出 -1。
示例 2:

输入: nums1 = [2,4], nums2 = [1,2,3,4].
输出: [3,-1]
解释:
    对于num1中的数字2，第二个数组中的下一个较大数字是3。
    对于num1中的数字4，第二个数组中没有下一个更大的数字，因此输出 -1。
注意:

nums1和nums2中所有元素是唯一的。
nums1和nums2 的数组大小都不超过1000。

## 参考文章
- []()
***
## 题解
### 我的题解
```c++
class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& nums1, vector<int>& nums2) {
        vector<int> res;
        int len2 = nums2.size();
        for (int &i : nums1) {
            int j = 0;
            for (; j < len2; j++) {
                if (nums2[j] == i) {
                    break;
                }
            }
            stack<int> tmpStack;
            tmpStack.push(i);
            for (int k = j; k < len2; k++) {
                if (nums2[k] > tmpStack.top()) {
                    res.push_back(nums2[k]);
                    tmpStack.push(nums2[k]);
                    break;
                }
            }
            if (tmpStack.top() == i) {
                res.push_back(-1);
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
    vector<int> nextGreaterElement(vector<int>& findNums, vector<int>& nums) {
        vector<int> res;
        stack<int> st;
        unordered_map<int, int> m;
        for (int num : nums) {
            while (!st.empty() && st.top() < num) {
                m[st.top()] = num;
              	st.pop();
            }
            st.push(num);
        }
        for (int num : findNums) {
            res.push_back(m.count(num) ? m[num] : -1);
        }        
        return res;
    }
};
```
## 反思

- 牛逼，就是说遇到一个大数就遍历整个栈进行查看，OK的话就建立映射

# 844. 比较含退格的字符串

## 题目

给定 S 和 T 两个字符串，当它们分别被输入到空白的文本编辑器后，判断二者是否相等，并返回结果。 # 代表退格字符。

 

示例 1：

输入：S = "ab#c", T = "ad#c"
输出：true
解释：S 和 T 都会变成 “ac”。
示例 2：

输入：S = "ab##", T = "c#d#"
输出：true
解释：S 和 T 都会变成 “”。
示例 3：

输入：S = "a##c", T = "#a#c"
输出：true
解释：S 和 T 都会变成 “c”。
示例 4：

输入：S = "a#c", T = "b"
输出：false
解释：S 会变成 “c”，但 T 仍然是 “b”。


提示：

1 <= S.length <= 200
1 <= T.length <= 200
S 和 T 只含有小写字母以及字符 '#'。

## 参考文章

- [LeetCode\] 844. Backspace String Compare 退格字符串比较](https://www.cnblogs.com/grandyang/p/10447783.html)
***
## 题解
### 我的题解

```c++
class Solution {
public:
    bool backspaceCompare(string S, string T) {
        if (backspace(S) == backspace(T)) {
            return true;
        } else {
            return false;
        }
    }
     string backspace(string str) {
        string res = "";
        for (char &c : str) {
            if (c == '#') {
                if (!res.empty()) {
                    res.pop_back();
                }
            } else {
                res.push_back(c);
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
    bool backspaceCompare(string S, string T) {
        string s = "", t = "";
        for (char c : S) c == '#' ? s.size() > 0 ? s.pop_back() : void() : s.push_back(c);
        for (char c : T) c == '#' ? t.size() > 0 ? t.pop_back() : void() : t.push_back(c);
        return s == t;
    }
};
```
## 反思

- 这道题给了我们两个字符串，里面可能会有井号符#，这个表示退格符，键盘上的退格键我们应该都很熟悉吧，当字打错了的时候，肯定要点退格键来删除的。当然也可以连续点好几下退格键，这样就可以连续删除了，在例子2和3中，也确实能看到连续的井号符。题目搞懂了之后，就开始解题吧，博主最先想的方法就是对S和T串分别处理完退格操作后再进行比较，那么就可以使用一个子函数来进行字符串的退格处理，在子函数中，我们新建一个结果 res 的空串，然后遍历输入字符串，当遇到退格符的时候，判断若结果 res 不为空，则将最后一个字母去掉；若遇到的是字母，则直接加入结果 res 中即可。这样S和T串同时处理完了之后，再进行比较即可，参见代码如下：


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