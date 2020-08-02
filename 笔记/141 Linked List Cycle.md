141. Linked List Cycle

Given a linked list, determine if it has a cycle in it.

To represent a cycle in the given linked list, we use an integer `pos` which represents the position (0-indexed) in the linked list where tail connects to. If `pos` is `-1`, then there is no cycle in the linked list.

 

**Example 1:**

```
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

**Example 2:**

```
Input: head = [1,2], pos = 0
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the first node.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png)

**Example 3:**

```
Input: head = [1], pos = -1
Output: false
Explanation: There is no cycle in the linked list.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png)

**解法1**	hashset

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
        unordered_map<ListNode*, bool>vis;
        ListNode* p = head;
        while(p){
            if(!vis[p]){
                vis[p] = true;
            }else{
                return true;
            }
            p = p->next;
        }
        return false;
    }
};
```

**解法2**	双指针

```c++
class Solution {
public:
    bool hasCycle(ListNode *head) {
        unordered_map<ListNode*, bool>vis;
        if(head == NULL || head->next == NULL)return false;
        ListNode* p = head, *pp = head->next;
        while(p != pp){
            if(p == NULL || pp == NULL || pp->next == NULL)return false;
            p = p->next;
            pp = pp->next->next;
        }
        return true;
    }
};
```

