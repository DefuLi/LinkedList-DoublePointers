# LinkedList-DoublePointers
链表的练习题可以在LeetCode官网上找到[专项练习](https://leetcode-cn.com/explore/learn/card/linked-list/)<br>
1) 与数组不同，我们无法在常量时间内访问单链表中的随机元素。 如果我们想要获得第 i 个元素，我们必须从头结点逐个遍历。 我们按索引来访问元素平均要花费 O(N) 时间，其中 N 是链表的长度。<br>
2) 链表结构不善于检索操作，但是对于删除操作链表的时间复杂度是O(1)，可以在常量级别内解决。<br>

## 环形链表
给定一个链表，判断链表中是否有环。为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。<br>
```java
输入：head = [3,2,0,-4], pos = 1
输出：true
解释：链表中有一个环，其尾部连接到第二个节点。
```
判断一个链表中是否有环，可以使用双指针技巧解决。一个安全的选择是每次移动慢指针一步，而移动快指针两步。每一次迭代，快速指针将额外移动一步。如果环的长度为 M，经过 M 次迭代后，快指针肯定会多绕环一周，并赶上慢指针。<br>
在本道题中，我们同样设置两个指针，一个指针每次走一步，另一个指针每次走两步。这样如果有环的话，在慢指针迭代完一圈的时候两指针肯定相遇。<br>
```java
package practice;

// 环形链表
public class HasCycle {
    public static void main(String[] args) {
        ListNode head = new ListNode(-21);
        ListNode node1 = new ListNode(10);
        ListNode node2 = new ListNode(17);
        ListNode node3 = new ListNode(8);
        ListNode node4 = new ListNode(4);
        ListNode node5 = new ListNode(26);
        ListNode node6 = new ListNode(5);
        ListNode node7 = new ListNode(35);
        ListNode node8 = new ListNode(33);
        ListNode node9 = new ListNode(-7);
        ListNode node10 = new ListNode(-16);
        ListNode node11 = new ListNode(27);
        ListNode node12 = new ListNode(-12);
        ListNode node13 = new ListNode(6);
        ListNode node14 = new ListNode(29);
        ListNode node15 = new ListNode(-12);
        ListNode node16 = new ListNode(5);
        ListNode node17 = new ListNode(9);
        ListNode node18 = new ListNode(20);
        ListNode node19 = new ListNode(14);
        ListNode node20 = new ListNode(14);
        ListNode node21 = new ListNode(2);
        ListNode node22 = new ListNode(13);
        ListNode node23 = new ListNode(-24);
        ListNode node24 = new ListNode(21);
        ListNode node25 = new ListNode(23);
        ListNode node26 = new ListNode(-21);
        ListNode node27 = new ListNode(5);
        head.next = node1;
        node1.next = node2;
        node2.next = node3;
        node3.next = node4;
        node4.next = node5;
        node5.next = node6;
        node6.next = node7;
        node7.next = node8;
        node8.next = node9;
        node9.next = node10;
        node10.next = node11;
        node11.next = node12;
        node12.next = node13;
        node13.next = node14;
        node14.next = node15;
        node15.next = node16;
        node16.next = node17;
        node17.next = node18;
        node18.next = node19;
        node19.next = node20;
        node20.next = node21;
        node21.next = node22;
        node22.next = node23;
        node23.next = node24;
        node24.next = node25;
        node25.next = node26;
        node26.next = node27;
        node27.next = null;

        HasCycle obj = new HasCycle();
        System.out.println(obj.hasCycle(head));

        /**
         ListNode temp = new ListNode(1);
         ListNode temp2 = new ListNode(2);
         temp.next = temp2;
         System.out.println(temp.next.next.next);  // 空指针异常
         */
    }

    public boolean hasCycle(ListNode head) {
        if(head == null) return false;
        ListNode slow = head;
        ListNode fast = head;
        slow = head.next;
        if(head.next == null) return false;
        fast = head.next.next;
        if(slow == null || fast == null) return false;
        if (slow == fast) return true;
        while (slow != fast){
            if(slow == null || fast == null) return false;
            slow = slow.next;
            if(slow.next == null || fast.next == null) return false;

            fast = fast.next.next;
        }
        return true;
    }
}
```
## 环形链表II
给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。<br>
为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。<br>
```java
输入：head = [3,2,0,-4], pos = 1
输出：tail connects to node index 1
解释：链表中有一个环，其尾部连接到第二个节点。
```
相对于上一个题而言，本题的难度有所增加。不仅要判断该链表是否有环，还要判断环入口的位置是哪个。解决这个问题有个很巧妙的地方，就是判断完是否有环结构后，此时如果让慢指针赋值为head节点，快指针继续在相遇节点，快慢指针此时以每次一步的速度进行迭代，再次相遇的地方就是环入口的地方。<br>
这个解法，可以使用简单的数学设x进行求解。<br>
```java
package practice;

// 环形链表Ⅱ
public class DetectCycle {
    public static void main(String[] args) {
        ListNode head = new ListNode(3);
        ListNode node1 = new ListNode(2);
        ListNode node2 = new ListNode(0);
        ListNode node3 = new ListNode(-4);
        head.next = node1;
        node1.next = node2;
        node2.next = node3;
        node3.next = node1;

        DetectCycle obj = new DetectCycle();
        System.out.println(obj.detectCycle(head).val);
    }

    public ListNode detectCycle(ListNode head) {
        if(head == null) return null;
        ListNode slow = head;
        ListNode fast = head;
        slow = head.next;
        if(head.next == null) return null;
        fast = head.next.next;
        if(slow == null || fast == null) return null;
        if (slow == fast) return slow;
        while (slow != fast){
            if(slow == null || fast == null) return null;
            slow = slow.next;
            if(slow.next == null || fast.next == null) return null;

            fast = fast.next.next;
        }
        slow = head;
        while (slow != fast){
            slow = slow.next;
            fast = fast.next;
        }
        return slow;
    }
}
```
## 相交链表
判断两个链表相交的起始节点，该题的具体题目可以点击此[链接](https://leetcode-cn.com/explore/learn/card/linked-list/194/two-pointer-technique/746/)。<br>
```java
输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
输出：Reference of the node with value = 8
输入解释：相交节点的值为 8 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。
```
下面的代码是一种比较笨的方法，有点暴力破解的嫌疑，不可取。好的解决方法是先算出两条链表的长度，然后移除较长的链表多出来的部分，此时同步遍历两条链表，便可解决该问题。<br>
```java
package practice;
// 相交链表
/**
 * 好的解决方案是先算出来两条链表的长度，
 * 较长的链表从头节点去除多出来的部分，
 * 然后两个链表同步遍历。
 */
public class GetIntersectionNode {
    public static void main(String[] args) {
        ListNode headA = new ListNode(0);
        ListNode node1 = new ListNode(9);
        ListNode node2 = new ListNode(1);
        ListNode node3 = new ListNode(2);
        ListNode node4 = new ListNode(4);
        ListNode headB = new ListNode(3);
        headA.next = node1;
        node1.next = node2;
        node2.next = node3;
        node3.next = node4;
        headB.next = node3;
        GetIntersectionNode obj = new GetIntersectionNode();
        System.out.println(obj.getIntersectionNode(headA, headB).val);
    }
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode slow = headA;
        ListNode fast = headB;
//        ListNode flag = headB;
        while (slow != fast){
            if(slow == null) return null;
            if(fast == null) {
                slow = slow.next;
//                flag = flag.next;
                fast = headB;
            }else {
                fast = fast.next;
            }
        }
        return slow;
    }
}

```
## 删除链表的倒数第N个节点
给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。<br>
```java
给定一个链表: 1->2->3->4->5, 和 n = 2.

当删除了倒数第二个节点后，链表变为 1->2->3->5.
```
使用双指针技巧可以巧妙的解决这个问题，既然是要删除倒数第n个节点，我们首先让快指针从头往后走n步，然后让慢指针赋值为head节点，此时快指针和慢指针之间的间距就是n，然后快慢指针同时走到尾节点，慢指针所指向的位置就是倒数第n个节点。<br>
```java
package practice;

// 删除链表的倒数第N个节点
public class RemoveNthFromEnd {
    public static void main(String[] args) {
        ListNode head = new ListNode(1);
        ListNode node1 = new ListNode(2);
        ListNode node2 = new ListNode(3);
        ListNode node3 = new ListNode(4);
        ListNode node4 = new ListNode(5);
        head.next = node1;
        node1.next = node2;
        node2.next = node3;
        node3.next = node4;
        RemoveNthFromEnd obj = new RemoveNthFromEnd();
        ListNode res = obj.removeNthFromEnd(head, 2);
        while (res != null) {
            System.out.println(res.val);
            res = res.next;
        }
    }

    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode front = head;
        ListNode back = head;
        // 先判断要删除的是否为头节点
        for (int i = 0; i < n; i++) {
            front = front.next;
        }
        if (front == null) {
            head = head.next;
            return head;
        }
        while (front.next != null) {
            front = front.next;
            back = back.next;
        }
        back.next = back.next.next;
        return head;
    }
}
```
## 回文链表
请判断一个链表是否为回文链表。<br>
```java
输入: 1->2->2->1
输出: true
```
首先对一半的链表进行反转操作，然后分别保存前段链表的head节点和后段链表的head节点，同步遍历判断val值是否相等即可。<br>
```java
package practice;

import java.util.ArrayList;
import java.util.List;

// 回文链表
public class IsPalindrome {
    public static void main(String[] args) {
        ListNode head = new ListNode(1);
        ListNode node1 = new ListNode(2);
        ListNode node2 = new ListNode(3);
        ListNode node3 = new ListNode(4);
        ListNode nodeTemp = new ListNode(5);
        ListNode node4 = new ListNode(2);
        ListNode node5 = new ListNode(3);
        ListNode node6 = new ListNode(2);
        ListNode node7 = new ListNode(1);

        head.next = node1;
        node1.next = node2;
        node2.next = node3;
        node3.next = nodeTemp;
        nodeTemp.next = node4;
        node4.next = node5;
        node5.next = node6;
        node6.next = node7;
        node7.next = null;


        IsPalindrome obj = new IsPalindrome();
        System.out.println(obj.isPalindrome(head));
        /**
        List<ListNode> list = obj.getReversedList(head);
        ListNode res1 = list.get(0);
        ListNode res2 = list.get(1);
        while (res1 != null) {
            System.out.println(res1.val);
            res1 = res1.next;
        }
        while (res2 != null) {
            System.out.println(res2.val);
            res2 = res2.next;
        }
         */
    }

    public boolean isPalindrome(ListNode head) {
        if(head == null || head.next == null) return true;
        List<ListNode> list = getReversedList(head);
        ListNode res1 = list.get(0);
        ListNode res2 = list.get(1);
        while (res1 != null){
            if(res1.val != res2.val){
                return false;
            }
            res1 = res1.next;
            res2 = res2.next;
        }
        return true;
    }

    // 获取链表长度
    public int getLen(ListNode head) {
        int nums = 0;
        ListNode temp = head;
        while (temp != null) {
            nums++;
            temp = temp.next;
        }
        return nums;
    }

    // 对一半的链表进行逆序操作
    public List<ListNode> getReversedList(ListNode head) {
        List<ListNode> list = new ArrayList<>();
        int len = getLen(head);

        ListNode flag = head;
        ListNode temp;
        int i = 1;
        if (len % 2 == 0) {
            while (i < len / 2) {
                temp = flag.next.next;
                flag.next.next = head;
                head = flag.next;
                flag.next = temp;
                i++;
            }
            temp = flag.next;
            flag.next = null;
            list.add(head);
            list.add(temp);
        }else {
            while (i < len / 2) {
                temp = flag.next.next;
                flag.next.next = head;
                head = flag.next;
                flag.next = temp;
                i++;
            }
            temp = flag.next.next;
            flag.next = null;
            list.add(head);
            list.add(temp);
        }
        return list;
    }
}
```
## 扁平化多级双向链表
您将获得一个双向链表，除了下一个和前一个指针之外，它还有一个子指针，可能指向单独的双向链表。这些子列表可能有一个或多个自己的子项，依此类推，生成多级数据结构，如下面的示例所示。<br>
扁平化列表，使所有结点出现在单级双链表中。您将获得列表第一级的头部。<br>
```java
输入:
 1---2---3---4---5---6--NULL
         |
         7---8---9---10--NULL
             |
             11--12--NULL

输出:
1-2-3-7-8-11-12-9-10-4-5-6-NULL
```
对于这个问题，如果当前节点的child不为null，那么就需要访问其child，我使用一个栈来保存当前节点的next，以便访问完child后可以接着对拐点的next进行访问。<br>
```java
package practice;

import java.util.Stack;

// 扁平化多级双向链表
public class Flatten {
    public static void main(String[] args) {
        DoubleList node1 = new DoubleList(1);
        DoubleList node2 = new DoubleList(2);
        DoubleList node3 = new DoubleList(3);
        DoubleList node4 = new DoubleList(4);
        DoubleList node5 = new DoubleList(5);
        DoubleList node6 = new DoubleList(6);
        DoubleList node7 = new DoubleList(7);
        DoubleList node8 = new DoubleList(8);
        DoubleList node9 = new DoubleList(9);
        DoubleList node10 = new DoubleList(10);
        DoubleList node11 = new DoubleList(11);
        DoubleList node12 = new DoubleList(12);

        node1.next = node2;
        node2.prev = node1;
        node2.next = node3;
        node3.prev = node2;
        node3.next = node4;
        node4.prev = node3;
        node3.child = node7;
        node4.next = node5;
        node5.prev = node4;
        node5.next = node6;
        node6.prev = node5;

        node7.next = node8;
        node8.prev = node7;
        node8.next = node9;
        node9.prev = node8;
        node8.child = node11;
        node9.next = node10;
        node10.prev = node9;
        node11.next = node12;
        node12.prev = node11;
        Flatten obj = new Flatten();
        DoubleList res = obj.flatten(node1);
        while (res != null) {
            System.out.println(res.val);
            res = res.next;
        }
    }

    public DoubleList flatten(DoubleList head) {
        if (head == null || (head.next == null && head.child == null)) return head;
        Stack<DoubleList> stack = new Stack();
        DoubleList node = head;
        while (!stack.isEmpty() || node.next != null || node.child != null) {
            if (node.child != null) {
                if (node.next != null) stack.push(node.next);
                node.next = node.child;
                node.child.prev = node;
                node.child = null;
                node = node.next;
            } else {
                if (node.next == null && !stack.isEmpty()) {
                    DoubleList nextDoubleList = stack.pop();
                    node.next = nextDoubleList;
                    nextDoubleList.prev = node;
                    node = node.next;
                } else {
                    node = node.next;
                }
            }
        }
        return head;
    }
}

// 扁平化多级双向链表
class DoubleList {
    public int val;
    public DoubleList prev;
    public DoubleList next;
    public DoubleList child;

    DoubleList(int val) {
        this.val = val;
    }
}
```
## 复制带随机指针的链表
给定一个链表，每个节点包含一个额外增加的随机指针，该指针可以指向链表中的任何节点或空节点。该题的具体示意图[点此链接观看](https://leetcode-cn.com/explore/learn/card/linked-list/197/conclusion/766/)。<br>
要求返回这个链表的 深拷贝。 <br>
我们用一个由 n 个节点组成的链表来表示输入/输出中的链表。每个节点用一个 \[val, random_index] 表示：<br>
val：一个表示 Node.val 的整数。<br>
random_index：随机指针指向的节点索引（范围从 0 到 n-1）；如果不指向任何节点，则为  null 。<br>
```java
输入：head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
输出：[[7,null],[13,0],[11,4],[10,2],[1,0]]
```
对于该题，有两种方法可以解决。第一种方法就是使用HashMap方法，由于设计到深拷贝，在原链表和新链表直接可以使用HashMap进行映射，HashMap的泛型为<Node, Node>这样才可以。第二种方法的空间复杂度低于第一种，比较巧妙。第二种方法是在原链表的每个节点后创建一个一模一样的新节点，创建和原节点一样的规则，然后从混合链表中把新链表提取出来。<br>
```java
package practice;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.Map;

// 复制带随机指针的链表
public class CopyRandomList {
    public static void main(String[] args) {
        RandomList node1 = new RandomList(7);
        RandomList node2 = new RandomList(13);
        RandomList node3 = new RandomList(11);
        RandomList node4 = new RandomList(10);
        RandomList node5 = new RandomList(1);

        node1.next = node2;
        node1.random = null;
        node2.next = node3;
        node2.random = node1;
        node3.next = node4;
        node3.random = node5;
        node4.next = node5;
        node4.random = node3;
        node5.next = null;
        node5.random = node1;

        CopyRandomList obj = new CopyRandomList();
        RandomList res = obj.copyRandomList(node1);
        while (res != null) {
            System.out.println(res.val);
            if(res.random != null) {
                System.out.println(res.random.val);
            }else {
                System.out.println(res.random);
            }
            res = res.next;
        }
    }

    // 巧妙方法
    public RandomList copyRandomList1(RandomList head) {
        if(head == null) return null;
        RandomList node = head;
        while (node != null) {
            RandomList temp = new RandomList(node.val);
            RandomList nodeNext = node.next;
            node.next = temp;
            temp.next = nodeNext;
            node = node.next.next;
        }
        node = head;
        while (node != null) {
            if(node.random == null) {
                node.next.random = null;
            }else {
                node.next.random = node.random.next;
            }
            node = node.next.next;
        }
        node = head;
        RandomList res = head.next;
        while (node.next.next != null) {
            RandomList nodeNext = node.next;
            node.next = node.next.next;
            nodeNext.next = node.next.next;
            nodeNext = nodeNext.next;
            node = node.next;
        }
        node.next = null;
        return res;
    }
    // 使用HashMap<Node1, Node2>进行映射的维护。
    public RandomList copyRandomList(RandomList head) {
        if (head == null) return null;
        Map<RandomList, RandomList> map = new HashMap<>();
        RandomList node1 = head;  // 原链表
        RandomList node2 = new RandomList(head.val);  // 拷贝链表
        map.put(node1, node2);
        RandomList res = node2;
        while (node1 != null) {
            if (map.containsKey(node1.next)) {
                node2.next = map.get(node1.next);
            } else {
                if (node1.next != null) {
                    node2.next = new RandomList(node1.next.val);
                    map.put(node1.next, node2.next);
                } else {
                    node2.next = null;
                }
            }
            if (node1.random == null) {
                node2.random = null;
            } else {
                if (map.containsKey(node1.random)) {
                    node2.random = map.get(node1.random);
                } else {
                    node2.random = new RandomList(node1.random.val);
                    map.put(node1.random, node2.random);
                }
            }
            node1 = node1.next;
            node2 = node2.next;
        }
        return res;
    }

}

// 随机指针链表
class RandomList {
    int val;
    RandomList next;
    RandomList random;

    RandomList(int val) {
        this.val = val;
    }
}
```
