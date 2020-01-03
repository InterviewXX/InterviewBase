---
description: 堆的知识点和应用
---

# 堆

##  定义

* 一个完全二叉树
* 每个节点的值都大于等于（大顶堆）或小于等于（小顶堆）左右子节点的值

## 存储

由于堆是完全二叉树，所以一般用数组来存储。

![&#x7528;&#x6570;&#x7EC4;&#x8868;&#x793A;&#x5806;](../../../.gitbook/assets/image%20%2818%29.png)

**数组中下标为 i 的节点的左子节点，就是下标为 i∗2 的节点，右子节点就是下标为 i∗2+1 的节点，父节点就是下标为 i/2​ 的节点。**

## 堆化

### **插入元素-自下向上堆化**

 ****新插入的节点放入最后面，如果与父节点之间大小关系不满足定义，就交换两个节点，并继续比较 ，直到满足关系为止。

![&#x81EA;&#x4E0B;&#x5411;&#x4E0A;&#x5806;&#x5316;](../../../.gitbook/assets/image%20%288%29.png)

```text

public class Heap {
  private int[] a; // 数组，从下标1开始存储数据
  private int n;  // 堆可以存储的最大数据个数
  private int count; // 堆中已经存储的数据个数

  public Heap(int capacity) {
    a = new int[capacity + 1];
    n = capacity;
    count = 0;
  }

  public void insert(int data) {
    if (count >= n) return; // 堆满了
    ++count;
    a[count] = data;
    int i = count;
    while (i/2 > 0 && a[i] > a[i/2]) { // 自下往上堆化
      swap(a, i, i/2); // swap()函数作用：交换下标为i和i/2的两个元素
      i = i/2;
    }
  }
 }
```

###  删除堆顶元素-自顶向下堆化

堆顶元素存储着最大值（大顶堆）或者最小值（小顶堆）。一般移除堆顶元素来获得这个值。移除后需要对堆进行调整。

可以把最后一个元素放到堆顶，然后自顶向下进行调整，可以避免破坏完全二叉树结构。

 

![&#x5220;&#x9664;&#x5806;&#x9876;&#x5143;&#x7D20;&#x65F6;&#x53EF;&#x80FD;&#x7834;&#x574F;&#x5B8C;&#x5168;&#x4E8C;&#x53C9;&#x6811;&#x7ED3;&#x6784;](../../../.gitbook/assets/image%20%2811%29.png)

![&#x5220;&#x9664;&#x5143;&#x7D20;&#x65F6;&#x81EA;&#x9876;&#x5411;&#x4E0B;&#x8C03;&#x6574;](../../../.gitbook/assets/image%20%2812%29.png)

```text

public void removeMax() {
  if (count == 0) return -1; // 堆中没有数据
  a[1] = a[count];
  --count;
  heapify(a, count, 1);
}

private void heapify(int[] a, int n, int i) { // 自上往下堆化
  while (true) {
    int maxPos = i;
    //找到两个子节点中较大的那个，然后交换
    if (i*2 <= n && a[i] < a[i*2]) maxPos = i*2;
    if (i*2+1 <= n && a[maxPos] < a[i*2+1]) maxPos = i*2+1;
    if (maxPos == i) break;
    swap(a, i, maxPos);
    i = maxPos;
  }
}
```

### 

