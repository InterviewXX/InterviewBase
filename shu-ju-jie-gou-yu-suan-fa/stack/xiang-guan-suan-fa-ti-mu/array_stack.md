# 用数组实现栈

```text
public class ArrayStack implements Stack {

    private int[] array;
    private int size;


    ArrayStack(int cap) {
        array = new int[cap];
        size = 0;
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
        return array[--size];
    }

    @Override
    public boolean push(int data) {
        if (size == array.length) {
            //栈满
            return false;
        }
        array[size++] = data;
        return true;
    }

    @Override
    public int size() {
        return size;
    }

    @Override
    public void clear() {
        size = 0;
    }

    @Override
    public String toString() {
        StringBuilder sb = new StringBuilder();
        for (int i = size - 1; i >= 0; i--) {
            sb.append(array[i]);
            sb.append(",");
        }
        return sb.toString();
    }
}
```

