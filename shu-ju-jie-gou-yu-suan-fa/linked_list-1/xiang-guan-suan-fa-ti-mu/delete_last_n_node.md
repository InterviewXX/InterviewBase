# 删除倒数第n个结点

```text
/**
 * 删除倒数第n个结点
 * https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/
 * <p>
 * 思路：快慢指针
 */
public class DeleteLastXNode {


    /**
     * 返回删除后的链表
     *
     * @param list
     * @param n    倒数第n个
     * @return
     */
    static Node resolution(Node list, int n) {
        if (list == null || n <= 0) {
            return list;
        }

        Node slow = list;
        Node fast = list;
        int count = 0;
        while (fast != null && count < n) {
            fast = fast.next;
            count++;
        }

        if (count != n) {
            //长度不够
            return list;
        }

        //fast==null 时,头结点即为倒数第n个
        //删除头结点
        if (fast == null) {
            list = list.next;
            return list;
        }

        //fast!=null 删除链表中的结点
        //需要记录待删除结点的前驱结点
        Node pre = slow;
        //fast!=null 继续遍历
        while (fast != null) {
            fast = fast.next;
            pre = slow;
            slow = slow.next;
        }

        //删除链表中结点
        pre.next = slow.next;
        slow.next = null;
        return list;
    }


}
```

