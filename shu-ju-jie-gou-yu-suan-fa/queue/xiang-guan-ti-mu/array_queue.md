# 用数组实现队列

```text
public class ArrayQueue implements Queue {

    private int[] array;
    private int size;
    private int head;
    private int tail;


    ArrayQueue(int initCap) {
        array = new int[initCap];
        size = 0;
        head = 0;
        tail = 0;
    }


    @Override
    public boolean enqueue(int data) {
        if (size == array.length) {
            //队列已满
            return false;
        }
        if (tail == array.length) {
            //队列未满但是后面没有空间了，需要搬移数据
            for (int i = head; i < tail; i++) {
                array[i - head] = array[i];
            }
            head = 0;
            tail = head + size;
        }
        array[tail++] = data;
        size++;
        return true;
    }

    @Override
    public int deque() {
        if (isEmpty()){
            return -1;
        }
        int v = array[head++];
        size--;
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
        head = 0;
        tail = 0;
        size = 0;
    }
}
```

