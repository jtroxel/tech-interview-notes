**Trick:  Just keep pointers accurate, especially from init state**

\- I probably spent too much time trying to shorten the code, keep DRY.  Next time copy and past, etc to clean up.

```Java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 
 Merge Two Sorted Lists
   Splice together 2, sorted, linked lists
   - No new DS
   - Can compare 2 at a time
   
 EG:
    [1,2,4]
    [1,3,4] --> 1-> 1-> 2-> 3-> 4-> 4->
    
 EP
    [1,2,3,5]
    [1,3,4] --> 1-> 1-> 2-> 3-> 3-> 4-> 5->
    
 Et (1 list is empty, add on the rest)
    []
    [1,3,4] --> 1-> 3-> 4->
 
 
 Analysis
 - We zip them up
   - Zipper
   - Reuse list1, list2 for pointers to current items
 - Base:  one list empty, add rest to current
 - Compare 2 current pointers, set zipper.next
   - if zipper null, set zipper
 - Advance the next pointer
 
 
 
 */
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
      
      ListNode newHead = null;
      ListNode zipper = newHead;
      
      for (ListNode i = list1; i != null; i = i.next) System.out.print(i.val + "-> ");
      System.out.println();
      for (ListNode i = list2; i != null; i = i.next) System.out.print(i.val + "-> ");
      System.out.println();
      
      while (list1 != null || list2 != null) {
        // Compare pointers, set last
        ListNode lastUsed = compareNodes(list1, list2);
        zipper = initZipper(zipper, lastUsed);
        if (newHead == null) newHead = zipper;
        // Advance used
        if (list1 == lastUsed) {
          list1 = list1.next;
        } else {
          list2 = list2.next;
        }
        
        // for (ListNode i = newHead; i != null; i = i.next) System.out.print(i.val + "-> ");
        System.out.println();
        //zipper = zipper.next;
      }
      
      return newHead;
    }
  
  ListNode compareNodes(ListNode list1, ListNode list2) {
    if (list1 == null && list2 != null) return list2;
    if (list2 == null && list1 != null) return list1;
    
    if (list1.val <= list2.val) {
      // System.out.println("Next from 1 = " + list1.val);
      return list1;
    } else {
      // System.out.println("Next from 2 = " + list2.val);
      return list2;
    }
    
  }
  ListNode initZipper(ListNode zipper, ListNode list) {
    if (zipper == null) {
      return list;
    } else {
      zipper.next = list;
      return list;
    }
  }
}
```