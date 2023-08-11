[LeetCode > Problem List > 2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)

# 2. Add Two Numbers
###### Medium

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.


## (+)
Example 1:
![Details of the result](./img/2_addtwonumber1.png)
이미지 출처 - LeetCode > Problem List > 2. Add Two Numbers
```
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
```

Example 2:
```
Input: l1 = [0], l2 = [0]
Output: [0]
```
Example 3:
```
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
```

Constraints:
- The number of nodes in each linked list is in the range `[1, 100]`
- `0 <= Node.val <= 9`
- It is guaranteed that the list represents a number that does not have leading zeros.

***


## My submission
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
   public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
      ListNode head = new ListNode(0);
      ListNode tail = head;
      int carry = 0;

      while(l1 != null || l2 != null || carry != 0){
         int digit1 = (l1 != null)? l1.val : 0 ;
         int digit2 = (l2 != null)? l2.val : 0 ;
         
         int sum = digit1 + digit2 + carry;
         int digit = sum % 10;
         carry = sum / 10;
         
         tail.next = new ListNode(digit);
         tail = tail.next;
         
         l1 = (l1 != null) ? l1.next : null;
         l2 = (l2 != null) ? l2.next : null;
      }

      ListNode result = head.next;
      head.next = null;
      return result;
   }
}
```
[코드 참고](https://leetcode.com/problems/add-two-numbers/solutions/3675747/beats-100-c-java-python-beginner-friendly/)

***
이 문제를 풀기 위해 고민했지만, 문제를 이해하는 것만으로도 시간이 많이 사용될 정도로 지금의 나에게는 논리가 바로 그려지지 않는 문제였다. 
그래서 Solutions 코드를 참고하여 그 코드를 테스트하면서 문제와 해결 방법에 대하여 이해하는 시간을 가졌다.


### 코드의 논리에 대한 정리 

1. 필요한 변수 생성
   - 시작 포인터, 꼬리 포인터
2. 각 링크드리스트의 노드 값끼리 더하는 반복 작업
   - 반복문 조건 `l1 != null || l2 != null || carry != 0`
   - l1, l2 유효성 확인 후 새 변수에 값 저장
   - 더하기 작업
     - 사용된 변수 : sum, digit, carry
   - 새 노드 생성 및 꼬리 포인터 변경
   - l1, l2 각각 다음 노드로 이동
3. result 변수 생성
4. result 반환

### 회고
 링크드리스트에 대하여 문제를 보고 떠올리지 못한 것이 아주 아쉬웠다. 
 그래서 링크드리스트를 간단하게 구현해 보는 시간을 가져보는 어떨까 하고 생각한다.