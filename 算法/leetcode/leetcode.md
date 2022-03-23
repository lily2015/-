### 1

给你一个长度为 n 的整数数组 nums ，其中 nums 的所有整数都在范围 [1, n] 内，且每个整数出现 一次 或 两次 。请你找出所有出现 两次 的整数，并以数组形式返回。
你必须设计并实现一个时间复杂度为 O(n) 且仅使用常量额外空间的算法解决此问题。

链接：https://leetcode-cn.com/problems/find-all-duplicates-in-an-array

思路：所有整数都在范围 [1, n] 内，所以把数字对应的位置取反数，如果遍历到位置的数是负数，说明之前已经取过了

### 2
给你二叉树的根节点 root 和一个表示目标和的整数 targetSum 。判断该树中是否存在 根节点到叶子节点的路径，这条路径上所有节点值相加等于目标和 targetSum 。如果存在，返回 true ；否则，返回 false 。

叶子节点 是指没有子节点的节点。

链接：https://leetcode-cn.com/problems/path-sum
