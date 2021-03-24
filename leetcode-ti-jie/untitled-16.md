# 2.Add Two Numbers

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

![](https://gblobscdn.gitbook.com/assets%2F-MR3FOdSWIFY1yDqfjZ2%2F-MR9LJpQnXEYvY-uWumY%2F-MR9LsUbFAkqCwpCJ8Hn%2Faddtwonumber1.jpg?alt=media&token=fff2be1d-885b-4b0e-acce-e36615e8a101)

Example 1:

Input: l1 = \[2,4,3\], l2 = \[5,6,4\] Output: \[7,0,8\] Explanation: 342 + 465 = 807.

Example 2:

Input: l1 = \[0\], l2 = \[0\] Output: \[0\]

Example 3:

Input: l1 = \[9,9,9,9,9,9,9\], l2 = \[9,9,9,9\] Output: \[8,9,9,9,0,0,0,1\]

```text
class Solution{
    public ListNode addTwoNumbers(ListNode l1,ListNode l2 ){
        ListNode root = new ListNode(0);//创建一个新链表，表示得到的链表
        ListNode cursor = root; //根节点开始
        int carry = 0;  //carry只能是1或0，1代表两个所对应的节点相加超过10
        while(l1 != null || l2 != null || carry != 0){
            int l1val = l1 != null ?  l1.val : 0;
            int l2val = l2 != null ?  l2.val : 0;
            int sumval = l1val + l2val+ carry;
            carry = sumval / 10;
            cursor.next = new ListNode(sumval % 10);//新链表所对应节点的值
            cursor = cursor.next;//下一个节点
            if(l1 != null)
            l1 = l1.next;
            if(l2 != null)
            l2 = l2.next;
        }
        return root.next;
    }
}
```

emm,这题用到数据结构的知识，首先明白链表的框架，框架还是很简单的，举个例子,比如我们要用链表的每个节点。

看懂这个例子和上面题解的例子，自然就明白这个了。

