# 合并两个有序链表
将两个升序链表合并为一个新的 升序 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 
示例：

输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* ansnode = new ListNode(-1);//
        ListNode* pre = ansnode;
        while(l1 && l2) {
            if(l1->val <= l2->val) {
                pre->next = l1;
                l1 = l1->next;
            } else {
                pre->next = l2;
                l2 = l2->next;
            }
            pre = pre->next;
        }
        pre->next = (l1!=nullptr)?l1:l2;
        return ansnode->next;
    }
};
```

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var mergeTwoLists = function(l1, l2) {
    let ans = new ListNode();
    let cur = ans;
    while(l1 && l2) {
        if(l1.val <= l2.val) {
            cur.next = l1;
            l1 = l1.next;
        } else {
            cur.next = l2;
            l2 = l2.next;
        }
        cur = cur.next;
    }
    cur.next = l1?l1:l2;
    return ans.next;
};
```

总结：关于链表的问题,可以先声明一个头结点head，再声明一个cur的当前指针指向它，这个结点用来移动。(注意返回的是head.next)
以上是迭代法，由于要参加面试，故现只记住迭代。

# 两数之和
```cpp
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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int car = 0;
        ListNode* ans = new ListNode(0);//答案结点
        ListNode* cur = ans;//当前结点
        while(l1 || l2) {
            int m  = l1?l1->val:0;
            int n  = l2?l2->val:0;
            int sum = car + m + n;
            cur->next = new ListNode(sum%10);
            car = sum/10;
            cur = cur->next;
            if(l1) l1 = l1->next;
            if(l2) l2 = l2->next;
        }
        if(car > 0) {
            cur->next = new ListNode(car);
        }
        return ans->next;
    }
};
```

# 两数之和
```cpp
/*
*unordered_map无序的，利用哈希表来实现，搜索时间为log(n)
*map是在缺省的情况下，是有序的，利用二红黑树（一种平衡搜索树）,搜索时间为：O(1)为平均时间，最坏情况下的时间复杂度为O（n）
*/
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int len = nums.size();
        unordered_map<int,int> myMap;
        for(int i = 0; i < len; i++) {
            auto it = myMap.find(target-nums[i]);
            //如果不存在则返回myMap.end()
            if(it!=myMap.end()) {
                return {it->second , i};
            }
            //如果存在，则返回当前的迭代器。first是指key ， second是指的是value
            myMap.insert({nums[i] , i});
        }
        return {};
    }
};
```

