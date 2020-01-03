# 用链表实现栈

```text
public class LinkedStack implements Stack {

    //使用空头结点简化相关操作
    private Node top = new Node(Integer.MAX_VALUE);
    private int size = 0;
    private int initCap;

    public LinkedStack(int initCap) {
        this.initCap = initCap;
    }

    @Override
    public boolean isEmpty() {
        return size == 0;
    }

    @Override
    public int pop() {
        if (isEmpty()) {
            return -1;
        }
        Node popNode = top.next;
        top.next = popNode.next;
        popNode.next = null;
        size--;
        return popNode.data;
    }

    @Override
    public boolean push(int data) {
        if (size == initCap) {
            return false;
        }
        Node newNode = new Node(data);
        newNode.next = top.next;
        top.next = newNode;
        size++;
        return true;
    }

    @Override
    public int size() {
        return size;
    }

    @Override
    public String toString() {
        StringBuilder sb = new StringBuilder();
        Node n = top.next;
        while (n != null) {
            sb.append(n.data);
            sb.append(",");
            n = n.next;
        }
        return sb.toString();
    }

    @Override
    public void clear() {
        //清理数据
        while (top.next != null) {
            Node n = top.next;
            top.next = n.next;
            n.next = null;
        }
        size = 0;

    }


    static class Node {
        Node(int data) {
            this.data = data;
        }

        int data;
        Node next;
    }
}
```

