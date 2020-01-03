# 实现循环队列

```text
/**
 * 循环队列
 */
public class CircularQueue implements Queue {

    private int[] array;
    private int size;
    private int head;
    private int tail;


    public CircularQueue(int initCap) {
        array = new int[initCap + 1];
        size = 0;
        head = 0;
        tail = 0;
    }

    @Override
    public boolean enqueue(int data) {
        //注意队列已满的条件
        if ((tail + 1) % array.length == head) {
            return false;
        }
        array[tail] = data;
        size++;
        tail = (tail + 1) % array.length;
        return true;
    }

    @Override
    public int deque() {
        if (isEmpty()) {
            return -1;
        }
        int v = array[head];
        head = (head + 1) % array.length;
        size++;
        return v;
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
        size = 0;
        tail = head;
    }
}
```

