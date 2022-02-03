---
title: "Linked List"
date: 2022-01-30T10:54:23-08:00
draft: true
---



<!--more-->

## 1. Operations on Linked List

### Delete



### Reverse

e.g. [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

Solution 1: Iterative

```C++
ListNode* reverseList(ListNode* head) {
  ListNode *pre=nullptr;
  while(head){
    ListNode* next=head->next;
    head->next=pre;
    pre=head;
    head=next;
  }
  return pre;
}
// Time Complexity: O(n)
// Space Complexity: O(1)
```

Solution 2: Recursive

```C++
ListNode* reverseList(ListNode* head) {
  if(head==nullptr || head->next==nullptr) return head;
  ListNode* p=reverseList(head->next);
  head->next->next=head;
  head->next=nullptr;
  return p;   
}
// Time Complexity: O(n)
// Space Complexity: O(n)
```

`reverseList(head->next)` returns the reversed linked list, the head of this linked list before reversed is `head->next`. Next, we should add `head` to the end of the reversed linked list. This is exactly what `head->next->next=head` does.

e.g. [25. Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group/)

**Reverse specific range of a linked list**

```C++
vector<ListNode*> reverseRange(ListNode* head, ListNode* tail){
  ListNode *pre=tail->next, *p=head;
  while(pre!=tail){
    ListNode *next=p->next;
    p->next=pre;
    pre=p;
    p=next;
  }
  return vector<ListNode*>{tail, head};
}
```



### Merge

e.g. [2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)

Two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contains a single digit.

```C++
ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
  int carry=0;
  ListNode *ptr1=l1, *ptr2=l2;
  ListNode *res=new ListNode(0, nullptr);
  ListNode *ptr=res;
  while(ptr1 || ptr2 || carry!=0){
    if(ptr1){
      carry+=ptr1->val;
      ptr1=ptr1->next;
    }
    if(ptr2){
      carry+=ptr2->val;
      ptr2=ptr2->next;
    }
    ListNode *cur=new ListNode(carry%10, nullptr);
    carry/=10;
    ptr->next=cur;
    ptr=ptr->next;
  }
  return res->next;
}
```

Points:

* Use dump node to make code concise. With dump node, inserting the first node to an empty linked list is not a special case.
* `while(ptr1 || ptr2 || carry!=0)` makes the code elegant and concise.

**Similar problems:**

[21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)

## 2. Some Tricks

### Others

e.g. [138. Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer/)

Copy a linked list whose node contains an extra pointer which points to a random node in this linked list.

A nice solution is to inserting the clone node after its original node. Then the random pointer in the clone node points to its original random pointer's next node, which is exactly the corresponding clone node. Then we extract the clone node from the linked list and recover original node.

