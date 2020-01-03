# 合并两个有序链表

```text
/**
 * 合并两个有序(升序)链表
 */
public class MergeSortedLinkedList {


    /**
     * 循环解法
     *
     * @param list1 有序链表1
     * @param list2 有序链表2
     * @return 合并后的链表
     */
    static Node resolution(Node list1, Node list2) {

        if (list1 == null) {
            return list2;
        }
        if (list2 == null) {
            return list1;
        }

        Node p1 = list1;
        Node p2 = list2;
        Node result;
        Node cur;

        //可以利用空的头结点来简化
        if (p1.data > p2.data) {
            result = p2;
            p2 = p2.next;
        } else {
            result = p1;
            p1 = p1.next;
        }
        cur = result;

        while (p1 != null && p2 != null) {
            if (p1.data > p2.data) {
                cur.next = p2;
                p2 = p2.next;
            } else {
                cur.next = p1;
                p1 = p1.next;
            }
            cur = cur.next;
        }
        if (p1 == null) {
            cur.next = p2;
        } else {
            cur.next = p1;
        }

        return result;
    }

    static Node resolutionSimple(Node list1, Node list2) {
        if (list1 == null) {
            return list2;
        }

        if (list2 == null) {
            return list1;
        }

        Node fakeHead = new Node(Integer.MAX_VALUE);
        Node cur = fakeHead;

        while (list1 != null && list2 != null) {
            if (list1.data > list2.data) {
                cur.next = list2;
                list2 = list2.next;
            } else {
                cur.next = list1;
                list1 = list1.next;
            }
            cur = cur.next;
        }

        if (list1 == null) {
            cur.next = list2;
        } else {
            cur.next = list1;
        }

        return fakeHead.next;
    }


    /**
     * 递归版本
     */
    static Node resolutionByRecursion(Node list1, Node list2) {
        //递归终止条件
        if (list1 == null) {
            return list2;
        }

        if (list2 == null) {
            return list1;
        }


        if (list1.data > list2.data) {
            list2.next = resolutionByRecursion(list2.next, list1);
            return list2;
        } else {
            list1.next = resolutionByRecursion(list1.next, list2);
            return list1;
        }
    }
}
```

