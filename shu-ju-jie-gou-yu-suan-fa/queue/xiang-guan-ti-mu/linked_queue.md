# 用链表实现队列

```text
public class LinkedQueue implements Queue {
    private int initCap;
    private int size;
    //空数据的头结点，用于简化操作
    //头结点作为队列的尾部
    private Node tail = new Node(-1);
    private Node head = tail;

    public LinkedQueue(int initCap) {
        this.initCap = initCap;
        size = 0;
    }

    @Override
    public boolean enqueue(int data) {
        if (size == initCap) {
            return false;
        }
        Node n = new Node(data);
        head.next = n;
        head = n;
        size++;
        return true;
    }

    @Override
    public int deque() {
        if (isEmpty()) {
            return -1;
        }
        Node n = tail.next;
        tail.next = n.next;
        if (n == head) {
            //只有一个结点情况
            head = tail;
        }
        size--;
        return n.data;
    }

    @Override
    public boolean isEmpty() {
        return size == 0;
    }

    @Override
    public int size() {
        return size;
    }

    @Override
    public void clear() {
        head = tail;
        Node n = tail;
        while (n.next != null) {
            Node t = n.next;
            n.next = t.next;
            t.next = null;
        }
        size = 0;
    }


    static class Node {
        int data;
        Node next;

        Node(int data) {
            this.data = data;
        }
    }
}
```

