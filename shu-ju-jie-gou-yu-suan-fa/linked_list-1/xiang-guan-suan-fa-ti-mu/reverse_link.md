# 反转链表

```text
/**
 * 单链表反转
 * <p>
 * 思路：从头结点开始，对每个结点采用头插法插入一个新的链表
 */
public class ReverseLinkedList {


    /**
     * 循环解法
     *
     * @param list 待反转的链表
     * @return 反转后的链表头结点
     */
    public static Node resolution(Node list) {
        //链表为空或只有一个结点，直接返回
        if (list == null || list.next == null) {
            return list;
        }

        //新链表头结点
        Node newHead = null;
        while (list != null) {
            //当前结点的下一个结点
            Node next = list.next;
            //将结点的 next 指向前一个结点
            list.next = newHead;
            //头结点迁移
            newHead = list;
            list = next;
        }
        return newHead;
    }


    /**
     * 递归解法
     *
     * @param list
     * @return
     */
    public static Node resolutionByRecursion(Node list) {
        //如果是空链表，直接返回
        if (list == null) {
            return null;
        }

        //如果是只有一个结点的链表，也直接返回
        //这个条件同时也是递归的终止条件
        if (list.next==null){
            return list;
        }

        //以上两句可以合并为
//        if (list == null || list.next == null) {
//            return list;
//        }

        //通过递归反转当前结点后的节点
        Node reversedList = resolutionByRecursion(list.next);

        //此时 list.next 指向反转的链表的尾结点
        //假设原链表为1->2->3->4->null，当前结点list为1
        //则此时反转后的部分为 4->3->2->null
        //而此时 list.next 指向 2

        //将当前结点连接到反转后的链表的末尾，此时反转的链表为4->3->2->1
        list.next.next = list;
        //但当前结点1的next依然指向 2，因此需要把当前结点的 next 指向 null
        list.next = null;
        //通过此打印语句可以知道，返回的 reversedList 一直是原链表的尾结点
        //通过画图搞清楚递归过程中的指向，特别是知道当前结点的next指向的是反转后的链表的尾结点，就比较好理解了
//        System.out.println("反转后的链表头结点值为"+reversedList.data);
        return reversedList;
    }

}
```

