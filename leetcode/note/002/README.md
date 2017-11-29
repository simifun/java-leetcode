# [Add Two Numbers](https://leetcode.com/problems/add-two-numbers/description/)
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
</br>Output: 7 -> 0 -> 8

大致意思就是用单链表逆序表示的两个数求和，所以求和进位是往链表next位进位。
好了知道意思了就很好解决了。

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode result = new ListNode(0);
        ListNode p=l1,q=l2,now = result;
        int carry=0;
        while(p!=null||q!=null){
            int x = (p!=null) ? p.val:0;
            int y = (q!=null) ? q.val:0;
            int sum = x+y+carry;
            carry = sum%10;
            now.next = new ListNode(sum/10);
            
            if(p!=null) p=p.next;
            if(q!=null) q=q.next;
            now=now.next;
        }
        if(carry>0){
            now.next = new ListNode(carry);
        }
        return result.next;
    }
}
```
时间复杂度O(max(m,n))，空间复杂度O(max(m,n))，m,n指两链表的长度。
