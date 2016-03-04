翻译：

```
给你两个表示两个非负数字的链表。数字以相反的顺序存储，其节点包含单个数字。将这两个数字相加并将其作为一个链表返回。

输入: (2 -> 4 -> 3) + (5 -> 6 -> 4)
输出: 7 -> 0 -> 8
```

原题：

```
You are given two linked lists representing two non-negative numbers. 
The digits are stored in reverse order and each of their nodes contain a single digit. 
Add the two numbers and return it as a linked list.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
```



C++

```
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
        int carry=0;
        ListNode* listNode=new ListNode(0);
        ListNode* p1=l1,*p2=l2,*p3=listNode;
        
        while(p1!=NULL|p2!=NULL)
        {
            if(p1!=NULL)
            {
                carry+=p1->val;
                p1=p1->next;
            }
            if(p2!=NULL)
            {
                carry+=p2->val;
                p2=p2->next;
            }
            p3->next=new ListNode(carry%10);
            p3=p3->next;
            carry/=10;
        }
        if(carry==1)
            p3->next=new ListNode(1);
        return listNode->next;  
    }
};
```


C#
```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int x) { val = x; }
 * }
 */
public class Solution
{
    public ListNode AddTwoNumbers(ListNode l1, ListNode l2)
    {
        int carry = 0;
        ListNode listNode= new ListNode(0);
        ListNode p1 = l1, p2 = l2, p3 = listNode;

        while (p1 != null || p2 != null)
        {
            if (p1 != null)
            {
                carry += p1.val;
                p1 = p1.next;
            }
            if (p2 != null)
            {
                carry += p2.val;
                p2 = p2.next;
            }
            p3.next = new ListNode(carry % 10);
            p3 = p3.next;
            carry /= 10;
        }
        if (carry == 1)
            p3.next = new ListNode(1);
        return listNode.next;
    }
}
```

Java

```
public class Solution {
	 public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
		 int carry=0;
		 ListNode listNode=new ListNode(0);
		 ListNode p1=l1,p2=l2,p3=listNode;
		 while(p1!=null||p2!=null){
			 if(p1!=null){
				 carry+=p1.val;
				 p1=p1.next;
			 }
			 if(p2!=null){
				 carry+=p2.val;
				 p2=p2.next;
			 }
			 p3.next=new ListNode(carry%10);
			 p3=p3.next;
			 carry/=10;
		 }
		 if(carry==1)
			 p3.next=new ListNode(1);
	     return listNode.next;  
	 }
}

```


C++（来源于网络）
```
class Solution {
public:
    ListNode *addTwoNumbers(ListNode *l1, ListNode *l2) {
        int carry=0;
        ListNode* res=new ListNode(0);
        ListNode* head = res;
        while (l1 && l2){
            res->next=new ListNode((l1->val+l2->val+carry)%10);
            carry = (l1->val+l2->val+carry)/10;
            l1=l1->next;
            l2=l2->next;
            res=res->next;
        }        
        while (l1){
            res->next=new ListNode((l1->val+carry)%10);
            carry = (l1->val+carry)/10;
            l1=l1->next;
            res=res->next;
        }        
        while (l2){
            res->next=new ListNode((l2->val+carry)%10);
            carry = (l2->val+carry)/10;
            l2=l2->next;
            res=res->next;
        }        
        if (carry>0){
            res->next = new ListNode(carry);
        }        
        return head->next;        
    }
};
```