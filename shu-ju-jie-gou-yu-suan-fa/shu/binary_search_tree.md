# 二叉查找树

### 概念

也叫二叉搜索树，对于树中每个节点，左子树的每个节点的值都小于这个节点的值，而右子树的每个节点的值都大于这个节点的值。

![&#x4E8C;&#x53C9;&#x67E5;&#x627E;&#x6811;&#x793A;&#x4F8B;](../../../.gitbook/assets/image%20%2820%29.png)

**中序遍历二叉查找树可以得到有序序列。**

### 查找

从根节点开始遍历，如果值小于指定值 ，那么从右子树继续搜索，否则从左子树进行搜索。

```text
public Node find(int data) {    
    Node p = tree;    
    while (p != null) {      
        if (data < p.data) {
            p = p.left;      
        }
        else if (data > p.data){
            p = p.right;
        }      
        else {
            return p;
        }    
    }    
    return null;  
}
```

### 插入

根据大小关系找到对应的父节点，然后插入。

```text
public void insert(int data) { 
    if (tree == null) { 
        tree = new Node(data); 
        return; 
    } 
    Node p = tree; 
    while (p != null) { 
        if (data > p.data) { 
            if (p.right == null) { 
                p.right = new Node(data); 
                return; 
            } 
            p = p.right; 
        } else { // data < p.data
            if (p.left == null) { 
                p.left = new Node(data); 
                return; 
            } 
            p = p.left; 
        } 
    }
}
```

### 删除

* 如果要删除的节点没有子节点，我们只需要直接将父节点中，指向要删除节点的指针置为 null。
* 如果要删除的节点只有一个子节点（只有左子节点或者右子节点），我们只需要更新父节点中，指向要删除节点的指针，让它指向要删除节点的子节点就可以了。
* 如果要删除的节点有两个子节点，这就比较复杂了。需要找到**这个节点的右子树中的最小节点，把它替换到要删除的节点上。然后再删除掉这个最小节点**，因为最小节点肯定没有左子节点（如果有左子结点，那就不是最小节点了），所以，我们可以应用上面两条规则来删除这个最小节点。

```text
public void delete(int data) {
  Node p = tree; // p 指向要删除的节点，初始化指向根节点
  Node pp = null; // pp 记录的是待删除节点的父节点
  while (p != null && p.data != data) {
    pp = p;
    if (data > p.data){
        p = p.right;
    } else {
        p = p.left;
    }
  }
  if (p == null) {
      return; // 没有找到
  }

  // 要删除的节点有两个子节点
  if (p.left != null && p.right != null) { // 查找右子树中最小节点
    Node minP = p.right;
    Node minPP = p; // minPP表示minP的父节点
    while (minP.left != null) {
      minPP = minP;
      minP = minP.left;
    }
    p.data = minP.data; // 将minP的数据替换到p中
    p = minP; // 下面就变成了删除minP了
    pp = minPP;
  }

  // 删除节点是叶子节点或者仅有一个子节点
  Node child; // p的子节点
  if (p.left != null){
      child = p.left;
  }  else if (p.right != null){
      child = p.right;
  } else {
      child = null;
  }

  if (pp == null) tree = child; // 删除的是根节点
  else if (pp.left == p) pp.left = child;
  else pp.right = child;
}
```

###  重复元素

可以把重复元素当成比它大的元素插入，查找时找到第一个后继续遍历右子树，这样可以把所有等于某个值的所有节点都找出来，代码实现也比较简单。

### 与哈希表对比

* 中序遍历即可得到有序数据，而哈希表需要再排序
* 哈希表存在扩容问题，并且冲突时性能不稳定，而平衡的二叉查找树可以把时间复杂度稳定在O\(logn\)
* 哈希表构造比较复杂，要考虑哈希函数、扩容、哈希冲突等，而二叉查找树实现起来比较简单 

