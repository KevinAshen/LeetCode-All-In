[TOC]
# 622. 设计循环队列

## 题目

设计你的循环队列实现。 循环队列是一种线性数据结构，其操作表现基于 FIFO（先进先出）原则并且队尾被连接在队首之后以形成一个循环。它也被称为“环形缓冲器”。

循环队列的一个好处是我们可以利用这个队列之前用过的空间。在一个普通队列里，一旦一个队列满了，我们就不能插入下一个元素，即使在队列前面仍有空间。但是使用循环队列，我们能使用这些空间去存储新的值。

你的实现应该支持如下操作：

MyCircularQueue(k): 构造器，设置队列长度为 k 。
Front: 从队首获取元素。如果队列为空，返回 -1 。
Rear: 获取队尾元素。如果队列为空，返回 -1 。
enQueue(value): 向循环队列插入一个元素。如果成功插入则返回真。
deQueue(): 从循环队列中删除一个元素。如果成功删除则返回真。
isEmpty(): 检查循环队列是否为空。
isFull(): 检查循环队列是否已满。


示例：

MyCircularQueue circularQueue = new MycircularQueue(3); // 设置长度为 3

circularQueue.enQueue(1);  // 返回 true

circularQueue.enQueue(2);  // 返回 true

circularQueue.enQueue(3);  // 返回 true

circularQueue.enQueue(4);  // 返回 false，队列已满

circularQueue.Rear();  // 返回 3

circularQueue.isFull();  // 返回 true

circularQueue.deQueue();  // 返回 true

circularQueue.enQueue(4);  // 返回 true

circularQueue.Rear();  // 返回 4

 

提示：

所有的值都在 0 至 1000 的范围内；
操作数将在 1 至 1000 的范围内；
请不要使用内置的队列库。

## 参考文章
- [LeetCode\] Design Circular Queue 设计环形队列](https://www.cnblogs.com/grandyang/p/9899034.html)
***
## 题解
### 我的题解
```c++
// 题目要求的是要不浪费空间的，所以需要k + 1
class MyCircularQueue {
public:
    /** Initialize your data structure here. Set the size of the queue to be k. */
    MyCircularQueue(int k) {
        size = k + 1;
        head = 0;
        tail = 0;
        data.resize(k + 1);
    }
    
    /** Insert an element into the circular queue. Return true if the operation is successful. */
    bool enQueue(int value) {
        if ((tail + 1) % size == head) {
            return false;
        }
        data[tail] = value;
        tail = (tail + 1) % size;
        return true;
    }
    
    /** Delete an element from the circular queue. Return true if the operation is successful. */
    bool deQueue() {
        if (head == tail) {
            return false;    
        }
        head = (head + 1) % size;
        return true;
    }
    
    /** Get the front item from the queue. */
    int Front() {
        if (head == tail) {
            return -1;    
        }
        return data[head];
    }
    
    /** Get the last item from the queue. */
    int Rear() {
        if (head == tail) {
            return -1;    
        }
        return data[(tail - 1 + size) % size];
    }
    
    /** Checks whether the circular queue is empty or not. */
    bool isEmpty() {
        if (head == tail) {
            return true;    
        }
        return false;
    }
    
    /** Checks whether the circular queue is full or not. */
    bool isFull() {
        if ((tail + 1) % size == head) {
            return true;
        }
        return false;
    }
    
private:
    vector<int> data;
    int size, head, tail;
};

/**
 * Your MyCircularQueue object will be instantiated and called as such:
 * MyCircularQueue* obj = new MyCircularQueue(k);
 * bool param_1 = obj->enQueue(value);
 * bool param_2 = obj->deQueue();
 * int param_3 = obj->Front();
 * int param_4 = obj->Rear();
 * bool param_5 = obj->isEmpty();
 * bool param_6 = obj->isFull();
 */
```

***
### 参考题解
```c++
class MyCircularQueue {
public:
    MyCircularQueue(int k) {
        size = k; head = k - 1; tail = 0; cnt = 0;
        data.resize(k);
    }
    bool enQueue(int value) {
        if (isFull()) return false;
        data[tail] = value;
        tail = (tail + 1) % size;
        ++cnt;
        return true;
    }
    bool deQueue() {
        if (isEmpty()) return false;
        head = (head + 1) % size;
        --cnt;
        return true;
    }
    int Front() {
        return isEmpty() ? -1 : data[(head + 1) % size];
    }
    int Rear() {
        return isEmpty() ? -1 : data[(tail - 1 + size) % size];
    }
    bool isEmpty() {
        return cnt == 0;
    }
    bool isFull() {
        return cnt == size;
    }
    
private:
    vector<int> data;
    int size, cnt, head, tail;
};
```
## 反思

- 还是从简单的做起，判空就看当前个数 cnt 是否为0，判满就看当前个数 cnt 是否等于 size。接下来取首尾元素，先进行判空，然后根据 head 和tail 取即可，记得使用上循环数组的性质，要对 size 取余。再来看进队列函数，先进行判满，tail 要移动到下一位，为了避免越界，我们使用环形数组的经典操作，加1之后对长度取余，然后将新的数字加到当前的tail位置，cnt 再自增1即可。同样，出队列函数先进行判空，队首位置 head 要向后移动一位，同样进行加1之后对长度取余的操作，到这里就可以了，不用真正的去删除数字，因为 head 和 tail 限定了我们的当前队列的范围，然后 cnt 自减1

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