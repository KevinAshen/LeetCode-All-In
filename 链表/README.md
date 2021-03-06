[TOC]
# 234.回文链表

## 题目

请判断一个链表是否为回文链表。

示例 1:

输入: 1->2
输出: false
示例 2:

输入: 1->2->2->1
输出: true
进阶：
你能否用 O(n) 时间复杂度和 O(1) 空间复杂度解决此题？

## 参考文章

- [王争评论区大神](https://github.com/andavid/leetcode-java/blob/master/note/234/README.md)
***
## 题解

### 我的题解
```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        if (head == NULL || head->next == NULL) {
      return true;
    }

    ListNode *prev = NULL;
    ListNode *slow = head;
    ListNode *fast = head;

    while (fast != NULL && fast->next != NULL) {
      //pre：前一个
      //slow：慢指针&&后一段链表的开头
      //fast：快指针，边界工具人
      //操作就是要把慢指针经过的逆置过来，所以让pre作为前一个，slow作为当前工具人，使用next去记录下一个，就是slow的下一位
      //变换时，先把前面的逆过来，slow再往下走
      fast = fast->next->next;
      ListNode *next = slow->next;
      slow->next = prev;
      prev = slow;
      slow = next;
    }

    if (fast != NULL) {
      //！=NULL的这个情况就是奇数的情况，此时，slow工具人站在中间，pre就位，因此要让slow往前一个
      slow = slow->next;
    }

    while (slow != NULL) {
      if (slow->val != prev->val) {
        return false;
      }
      slow = slow->next;
      prev = prev->next;
    }

    return true;
    }
};
```

***
### 参考题解
```c++
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
  public boolean isPalindrome(ListNode head) {
    if (head == null || head.next == null) {
      return true;
    }

    ListNode prev = null;
    ListNode slow = head;
    ListNode fast = head;

    while (fast != null && fast.next != null) {
      fast = fast.next.next;
      ListNode next = slow.next;
      slow.next = prev;
      prev = slow;
      slow = next;
    }

    if (fast != null) {
      slow = slow.next;
    }

    while (slow != null) {
      if (slow.val != prev.val) {
        return false;
      }
      slow = slow.next;
      prev = prev.next;
    }

    return true;
  }
}
```
## 反思

- 快慢指针找中点
- 链表逆置

# 206. 反转链表

## 题目

反转一个单链表。

示例:

输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
进阶:
你可以迭代或递归地反转链表。你能否用两种方法解决这道题？

## 参考文章
- [LeetCode官方题解](https://leetcode-cn.com/problems/reverse-linked-list/solution/fan-zhuan-lian-biao-by-leetcode/)
***
## 题解
### 我的题解
```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        
        ListNode *pre = NULL;
        ListNode *next = NULL;
        ListNode *pNode = head;
        
        while (pNode != NULL) {
            next = pNode->next;
            pNode->next = pre;
            pre = pNode;
            pNode = next;
        }
        
        return pre;
    }
};
```

***
### 参考题解
```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        
       if (head == NULL || head->next == NULL) return head;
        ListNode *p = reverseList(head->next);
        head->next->next = head;
        head->next = NULL;
        return p;
    }
};
```
## 反思

- 递归骚断腿，实在难悟
- 妙

# 141. 环形链表

## 题目

给定一个链表，判断链表中是否有环。

为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。

 

示例 1：

输入：head = [3,2,0,-4], pos = 1
输出：true
解释：链表中有一个环，其尾部连接到第二个节点。


示例 2：

输入：head = [1,2], pos = 0
输出：true
解释：链表中有一个环，其尾部连接到第一个节点。


示例 3：

输入：head = [1], pos = -1
输出：false
解释：链表中没有环。




进阶：

你能用 O(1)（即，常量）内存解决此问题吗？

## 参考文章
- [LeetCode官方题解](https://leetcode-cn.com/problems/linked-list-cycle/solution/huan-xing-lian-biao-by-leetcode/)
***
## 题解
### 我的题解
```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    bool hasCycle(ListNode *head) {
        if (head == NULL || head->next == NULL) {
            return false;
        }
        ListNode *slow = head;
        ListNode *fast = head;
        while (fast->next != NULL && fast->next->next != NULL) {
            slow = slow->next;
            fast = fast->next->next;
            if (slow->val == fast->val) {
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
public boolean hasCycle(ListNode head) {
    Set<ListNode> nodesSeen = new HashSet<>();
    while (head != null) {
        if (nodesSeen.contains(head)) {
            return true;
        } else {
            nodesSeen.add(head);
        }
        head = head.next;
    }
    return false;
}
```
## 反思

- 要想链表玩的溜，两根指针少不了

# 21. 两个有序的链表合并

## 题目

将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

示例：

输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/merge-two-sorted-lists
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

## 参考文章
- [LeetCode官方题解](https://leetcode-cn.com/problems/merge-two-sorted-lists/solution/he-bing-liang-ge-you-xu-lian-biao-by-leetcode/)
***
## 题解
### 我的题解
```c++
//这谁会呢
```

***
### 参考题解
```c++
//递归
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if (l1 == NULL) {
          	//这一步不仅是一开始的判空，更是后面当一个链表已经遍历到结束了
          	//就一直使用另一个里面的节点
            return l2;
        } 
        else if (l2 == NULL) {
            return l1;
        }
        else if (l1->val < l2->val) {
          	//由于从小到大，因此
            l1->next = mergeTwoLists(l1->next, l2);
            return l1;
        }
        else {
            l2->next = mergeTwoLists(l1, l2->next);
            return l2;
        }
    }
};

//迭代
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
      	//这等于就是添加哨兵的思想，使得不用考虑开头的数字，妙啊
        ListNode *prehead = new ListNode(-1);

      
        ListNode *prev = prehead;
        while (l1 != NULL && l2 != NULL) {
            if (l1->val <= l2->val) {
              	//把l1连上
                prev->next = l1;
              	//接下来要做的仅仅是把l1指针指向下一个
                l1 = l1->next;
            } else {
                prev->next = l2;
                l2 = l2->next;
            }
            prev = prev->next;
        }
        prev->next = l1 == NULL ? l2 :l1;

        return prehead->next;
    }
};
```
## 反思

- 还是想太复杂了，其实只要进行一下链接就行，不用考虑辣么多

# 19. 删除链表的倒数第N个节点

## 题目

给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。

示例：

给定一个链表: 1->2->3->4->5, 和 n = 2.

当删除了倒数第二个节点后，链表变为 1->2->3->5.
说明：

给定的 n 保证是有效的。

进阶：

你能尝试使用一趟扫描实现吗？

## 参考文章
- [LeetCode官方题解](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/solution/shan-chu-lian-biao-de-dao-shu-di-nge-jie-dian-by-l/)
***
## 题解
### 我的题解
```c++
//这谁会呢
```

***
### 参考题解
```c++
//两次遍历算法
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode *dummy = new ListNode(0);
        dummy->next = head;
        int length  = 0;
        ListNode *first = head;
        while (first != NULL) {
            length++;
            first = first->next;
        }
        length -= n;
        first = dummy;
        while (length > 0) {
            length--;
            first = first->next;
        }
        first->next = first->next->next;
        return dummy->next;
    }
};

//一次遍历法
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode *dummy = new ListNode(0);
        dummy->next = head;
        ListNode *first = dummy;
        ListNode *second = dummy;
        for (int i = 1; i <= n + 1; i++) {
            first = first->next;
        }
        while (first != NULL) {
            first = first->next;
            second = second->next;
        }
        second->next = second->next->next;
        return dummy->next;
    }
};
```
## 反思

- 这又啥难的，惊了
- 两个字 哨兵

# 876. 链表的中间结点

## 题目

给定一个带有头结点 head 的非空单链表，返回链表的中间结点。

如果有两个中间结点，则返回第二个中间结点。

 

示例 1：

输入：[1,2,3,4,5]
输出：此列表中的结点 3 (序列化形式：[3,4,5])
返回的结点值为 3 。 (测评系统对该结点序列化表述是 [3,4,5])。
注意，我们返回了一个 ListNode 类型的对象 ans，这样：
ans.val = 3, ans.next.val = 4, ans.next.next.val = 5, 以及 ans.next.next.next = NULL.
示例 2：

输入：[1,2,3,4,5,6]
输出：此列表中的结点 4 (序列化形式：[4,5,6])
由于该列表有两个中间结点，值分别为 3 和 4，我们返回第二个结点。


提示：

给定链表的结点数介于 1 和 100 之间。

## 参考文章
- [LeetCode官方题解](https://leetcode-cn.com/problems/middle-of-the-linked-list/solution/lian-biao-de-zhong-jian-jie-dian-by-leetcode/)
***
## 题解
### 我的题解
```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode *slowNode = head;
        ListNode *fastNode = head;
        while (fastNode->next != NULL && fastNode->next->next != NULL) {
            fastNode = fastNode->next->next;
            slowNode = slowNode->next;
        }
        if (fastNode->next != NULL) {
            slowNode = slowNode->next;
        }
        return slowNode;
    }
};
```

***
### 参考题解
```c++
//这要啥参考题解呢
```
## 反思

- 联动题目，回文链表

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