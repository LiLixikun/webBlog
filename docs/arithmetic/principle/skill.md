# 实战特训
- 计算中的计算机原理(位运算)
- 双指针技巧
- 递归思想
- 广度优先和深度优先
- 最常见的算法范式
    暴力法
    分治法
    回溯算法
    动态规划
    贪心算法
    分支界限法      

## 双指针技巧

双指针技巧可以分为两类,一类是 **快慢指针**,另一类是 **左右指针** . 前者解决主要是链表的问题,比如典型的判定链表是否包含还;后者主要解决数组(或者字符串)中的问题,比如二分查找

### 快慢指针的常见算法
快慢指针一般都初始化执行链表的头节点 head,前进时快指针 fast 在前,慢指针 solw 在后,巧妙解决一些链表的一些问题