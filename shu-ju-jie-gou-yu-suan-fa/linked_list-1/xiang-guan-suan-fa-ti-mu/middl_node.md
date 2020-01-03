# 获取中间结点

```text
/**
 * 求中间结点
 * <p>
 * 思路：采用两个指针，其中一个指针每次前进一个结点，另一个每次前进两个结点，当较快的指针到达链表尾结点时，
 * 慢指针指向的节点即为中间结点
 * <p>
 * 如果有两个中间结点，默认返回后面一个
 * <p>
 * 如果需要返回前面的节点，则需要一个变量 pre 记录慢指针的前一结点，并在偶数情况时返回 pre
 */
public class MiddleNode {

    public static void main(String[] args) {
        Node n1 = new Node(1);
        Node n2 = new Node(2);
        Node n3 = new Node(3);
        Node n4 = new Node(4);
        Node n5 = new Node(5);
        Node n6 = new Node(6);
        n1.next = n2;
        n2.next = n3;
        n3.next = n4;
        n4.next = n5;
        n5.next = n6;

    }

    /**
     * 结点树为偶数时返回中间结点的后一个
     */
    public static Node resolution1(Node list) {
        if (list == null || list.next == null) {
            return list;
        }

        Node slow = list;
        Node fast = list;
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        return slow;
    }


    /**
     * 结点数为偶数时返回中间结点的前一个
     */
    public static Node resolution2(Node list) {
        if (list == null || list.next == null) {
            return list;
        }
        Node slowNode = list;
        Node fastNode = list;
        //如果对于偶数情况需要返回前面的中间结点，使用 pre 记录慢指针的前结点
        Node pre = null;
        while (fastNode != null && fastNode.next != null) {
            fastNode = fastNode.next.next;
            pre = slowNode;
            slowNode = slowNode.next;
        }
        //奇数情况 fast.next==null
        //偶数情况 fast==null
        //如果对于偶数情况需要返回前面的中间结点，则返回 pre
        if (fastNode == null) {
            return pre;
        }
        return slowNode;
    }
}
```

