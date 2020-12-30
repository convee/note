
# 学习算法和刷题框架思维
[toc]
---

## 数据结构存储方式
### 数组（顺序存储）
- 紧凑连续存储，可以随机访问
- 通过索引快速找到对应元素
- 相对节约存储空间
- 正因为连续存储，内存空间必须一次性分配够，所以说数组如果要扩容，需要重新分配一块更大的空间，再把数据全部复制过去，时间复杂度 O(N)
- 如果想在数组中间进行插入和删除，每次必须搬移后面的所有数据以保持连续，时间复杂度 O(N)

### 链表（链式存储）
- 元素不连续，而是靠指针指向下一个元素的位置，所以不存在数组的扩容问题
- 如果知道某一元素的前驱和后驱，操作指针即可删除该元素或者插入新元素，时间复杂度 O(1)
- 正因为存储空间不连续，你无法根据一个索引算出对应元素的地址，所以不能随机访问
- 由于每个元素必须存储指向前后元素位置的指针，会消耗相对更多的储存空间

## 数据结构比较
### 链表

### 队列和栈
- 数组：处理扩容问题
- 链表：需要更多的内存空间存储节点指针

### 图
- 邻接表（链表）：省空间，操作效率不如邻接矩阵
- 邻接矩阵（二维数组）：判断连通性迅速，如果图稀疏很耗空间

### 散列表
- 通过散列函数把键映射到一个大数组中
- 拉链法需要链表特性，操作简单，需要额外的空间存储指针
- 线性探查法需要数组特性，以便连续寻址，不需要指针的存储空间，操作复杂

### 树
- 数组实现就是「堆」，「堆」是一个完全二叉树，用数组存储不需要节点指针，操作简单
- 链表实现是常见的树，因为不一定是完全二叉树，所以不适合用数组存储

### 字符串
### 数组和矩阵
### 图
### 位运算
## 数据结构的基本操作
### 遍历访问（增删改查）
#### 形式
- 线性（迭代）
- 非线性（递归）

#### 框架
- 数组遍历

```golang
func traverse(arr []int) {
    for (int i := 0; i < len(arr); i++) {
        // 迭代访问 arr[i]
    }
}
```
- 链表遍历

```golang
// 单链表
type ListNode struct{
    Val int
    Next *ListNode
}
// 遍历
func traverse1(head *ListNode) {
    for head != nil {
        // 迭代访问 head.Val
        head = head.Next
    }
}
// 递归
func traverse2(head *ListNode) {
    // 递归访问 head.Val
    traverse(head.Next);
}
```
- 二叉树遍历

```golang
/* 基本的二叉树节点 */
type TreeNode struct{
    Val int
    Left *TreeNode
    Right *TreeNode
}

func traverse(root *TreeNode) {
    traverse(root.Left);
    traverse(root.Right);
}
```

- N 叉树

```golang
//N 叉树结点
type TreeNode struct {
    Val int
    Children []*TreeNode
}
func traverse(root *TreeNode) {
    for _,child := range root.Children {
        traverse(child)
    }
}
```
## 算法思想
### 双指针
### 排序
### 贪心思想
### 二分查找
### 分治
### 搜索
### 动态规划
### 数学
