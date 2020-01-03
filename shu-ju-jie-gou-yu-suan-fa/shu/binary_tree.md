# 二叉树

二叉树中，每个节点最多只有两个子节点，即左子节点和右子节点。

### 满二叉树

所有的叶子节点都在最后一层。

![&#x6EE1;&#x4E8C;&#x53C9;&#x6811;&#x793A;&#x4F8B;](../../../.gitbook/assets/image%20%2817%29.png)

### 完全二叉树

叶子节点都分布在最后两层，最后一层的叶子节点靠左排列，且除了最后一层外，其它层叶子节点都达到最满。

![&#x5B8C;&#x5168;&#x4E8C;&#x53C9;&#x6811;&#x793A;&#x4F8B;](../../../.gitbook/assets/image%20%2821%29.png)

**完全二叉树适合使用数组存储**，对于下标为i的节点，下标 2\*i 的节点就是其左子节点，下标 2\*i+1 的节点就是其右子节点。

![&#x7528;&#x6570;&#x7EC4;&#x5B58;&#x50A8;&#x4E8C;&#x53C9;&#x6811;](../../../.gitbook/assets/image%20%2822%29.png)

### 二叉树的遍历

#### 前序遍历

先遍历根节点，再遍历左子树，后遍历右子树

```text
/**
 * 前序遍历
 *
 * @param root 树的根节点
 */
static void preOrder(TreeNode root) {
    if (root == null) {
        return;
    }
    //先遍历根节点
    System.out.println(root.value);
    preOrder(root.left);
    preOrder(root.right);
}
```

#### 中序遍历

先遍历左子树，在遍历根节点，最后遍历右子树。

```text
/**
 * 中序遍历
 *
 * @param root 树的根节点
 */
static void inOrder(TreeNode root) {
    if (root == null) {
        return;
    }
    inOrder(root.left);
    System.out.println(root.value);
    inOrder(root.right);
}
```

#### 后序遍历

先遍历左子树，后遍历右子树，最后遍历根节点。

```text
/**
 * 后序遍历
 *
 * @param root 树的根节点
 */
static void postOrder(TreeNode root) {
    if (root == null) {
        return;
    }
    postOrder(root.left);
    postOrder(root.right);
    System.out.println(root.value);
}
```

#### 层序遍历

按树的层级一层一层遍历（可以借助队列）。

```text
/**
 * 层序遍历
 *
 * @param root 树的根节点
 */
static void levelOrder(TreeNode root) {
    if (root == null) {
        return;
    }  
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    while (!q.isEmpty()) {
        TreeNode n = q.poll();
        System.out.println(n.value);
        if (n.left != null) {
            q.offer(n.left);
        }
        if (n.right != null) {
            q.offer(n.right);
        }
    }
}
```



