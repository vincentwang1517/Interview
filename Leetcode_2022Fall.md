## Important Concepts

#### No. 0072

[Remove Element](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0027.%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0.md)

## vector

#### No. 0209

[website](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0209.%E9%95%BF%E5%BA%A6%E6%9C%80%E5%B0%8F%E7%9A%84%E5%AD%90%E6%95%B0%E7%BB%84.md)

```c++
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        
        int ans = nums.size() + 1;
        int sums = 0;
        int pl = 0;
        
        for (int pr=0; pr<nums.size(); pr++) {
            sums += nums[pr];
            // update pl/sums/ans
            while (sums >= target) {
                ans = ans > pr-pl+1 ? pr-pl+1 : ans;
                sums -= nums[pl++];
            }
        }
        
        if (ans == nums.size() + 1) return 0;
        return ans;        
    }
};

// Sliding windows: Limit the upperbound
```



## Linked List

#### No. 0069

[website](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0024.%E4%B8%A4%E4%B8%A4%E4%BA%A4%E6%8D%A2%E9%93%BE%E8%A1%A8%E4%B8%AD%E7%9A%84%E8%8A%82%E7%82%B9.md)

```c++
class Solution {
public:
    ListNode* swapPairs(ListNode* head) 
    {
        if (!head) return head;
        ListNode* dummy_head = new ListNode(0, head);
        ListNode* p1 = dummy_head;
        ListNode* p2 = head;
        ListNode* p3 = head->next;
        ListNode* p4;
        
        while (p2 && p3) {
            p4 = p3->next;
            p1->next = p3;
            p2->next = p4;
            p3->next = p2;
            if (!p4) break;
            p1 = p2;
            p2 = p4;
            p3 = p4->next;
        }
        
        p1 = dummy_head->next;
        delete dummy_head;
        return p1;        
    }
};
```

#### No. 0019

[website](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0019.%E5%88%A0%E9%99%A4%E9%93%BE%E8%A1%A8%E7%9A%84%E5%80%92%E6%95%B0%E7%AC%ACN%E4%B8%AA%E8%8A%82%E7%82%B9.md)

```c++
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        if (n <= 0) return head;
        ListNode* dhead = new ListNode(0, head);
        ListNode* pslow = dhead, * pfast = dhead;
        // Move pfast n step
        while (n-- && pfast->next) pfast = pfast->next;
        if (n>-1) return head;
        // Move 2 pointer
        while (pfast->next) {
            pslow = pslow->next;
            pfast = pfast->next;
        }
        pslow->next = pslow->next->next;
        ListNode* new_head = dhead->next;        
        delete dhead;
        return new_head;
    }
};
```
## String

#### No.0151

[Reverse Words in a String](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0151.%E7%BF%BB%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2%E9%87%8C%E7%9A%84%E5%8D%95%E8%AF%8D.md)

#### No.0028

[KMP](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0028.%E5%AE%9E%E7%8E%B0strStr.md)

## Stack & Queue

#### No. 0233

[Implement Queue Using Stacks](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0232.%E7%94%A8%E6%A0%88%E5%AE%9E%E7%8E%B0%E9%98%9F%E5%88%97.md)

```c++
class MyQueue {
public:
    MyQueue() {
    }
    
    void push(int x) {
        st1.push(x);
    }
    
    int pop() {
        int tmp = this->peek();
        st2.pop();
        return tmp;
    }
    
    int peek() {
        if (st2.empty()) {
            while (!st1.empty()) {
                st2.push(st1.top());
                st1.pop();
            }
        }
        return st2.top();
    }
    
    bool empty() {
        return st1.empty() && st2.empty();
    }
private:
    stack<int> st1; // input stack
    stack<int> st2; // output stack
};
```

