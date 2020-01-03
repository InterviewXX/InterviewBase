# 检测单链表是否有环

```text
/**
 * 单链表中环的检测、环的长度、环的入口结点、环前长度
 * <p>
 * 思路：快慢指针，慢指针每次前进一个结点，快指针每次前进两个结点，如果两个指针相遇，则说明有环；
 * 两指针相遇后，记录相遇结点，慢指针继续前进，同时记录步数，直到再次到相遇结点，前进的步数为环的长度；
 * 求得环的长度后，再次采用快慢指针从头遍历，快指针先前进n个结点(n为环的长度)，之后两个结点一起前进，两指针相遇的结点即为环的入口；
 * 再次从头结点遍历，到环的入口之间的结点经历的结点个数，即为环前长度。
 */
public class CircleCheck {


    /**
     * 判断链表是否有环
     */
    static boolean hasCircle(Node list) {
        //空链表返回false
        if (list == null) {
            return false;
        }
        Node fast = list;
        Node slow = list;
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
            if (fast == slow) {
                //两个指针相遇，证明有环
                return true;
            }
        }
        return false;
    }

    /**
     * 判断链表是否有环，如果有则返回快慢指针相遇结点
     */
    private static Node hasCircleReturnNode(Node list) {
        //空链表返回false
        if (list == null) {
            return null;
        }
        Node fast = list;
        Node slow = list;
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
            if (fast == slow) {
                //两个指针相遇，证明有环
                return slow;
            }
        }
        return null;
    }


    /**
     * 求链表中环的长度
     */
    static int circleLength(Node list) {
        Node p = hasCircleReturnNode(list);
        if (p == null) {
            //无环返回0
            return 0;
        }
        int length = 0;
        Node n = p;
        do {
            n = n.next;
            length++;
        } while (n != p);
        return length;
    }

    /**
     * 求链表中环的入口结点
     * @param list
     * @return
     */
    static Node circleEntrance(Node list) {
        int circleLength = circleLength(list);
        if (circleLength == 0) {
            return null;
        }

        Node slow = list;
        Node fast = list;

        for (int i = 0; i < circleLength; i++) {
            fast = fast.next;
        }

        while (slow != fast) {
            slow = slow.next;
            fast = fast.next;
        }
        return slow;
    }


    /**
     * 求链表的环前长度，如果无环返回链表总长度
     * @param list
     * @return
     */
    public static int lengthBeforeCircleEntrance(Node list) {
        Node entrance = circleEntrance(list);

        Node p = list;
        int length = 0;
        while (p != entrance) {
            length++;
            p = p.next;
        }
        return length;
    }
}
```

