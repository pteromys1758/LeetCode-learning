# LeetCode 学习记录
[TOC]
## 剑指Offer
### 第1天2022/7/9
completed two questions：
- 剑指 Offer 09. 用两个栈实现队列
- 剑指 Offer 30. 包含min函数的栈

知识点：
- 栈：先进后出 first in last output  
- 队列：先进先出
- python列表[]使用
```
a = [1, 2, 3]
print("输出链表最后一个",a[-1])
```

### 第2天2022/7/10
- 剑指 Offer 06. 从尾到头打印链表
  - 利用递归
  - 利用栈。栈是先进后出，说明递归其实就是栈。[::]使用，切片
  ```
  [起点:终点（不可到达）:变化量]
  ```
- 剑指 Offer 24. 反转链表
  - 利用递归。有点难思考。重要的是递归公式和截止条件。
  - 双指针，迭代。截止条件没有想清楚。
- 剑指 Offer 35. 复杂链表的复制
  - 哈希表，字典
  - 拼接 + 拆分。空间更少，时间相同

### 第3天2022/7/11
- 剑指 Offer 05. 替换空格
  - 在 Python 和 Java 等语言中，字符串都被设计成「不可变」的类型，即无法直接修改字符串的某一位字符，需要新建一个字符串实现。
  - 在 C++ 语言中， string 被设计成「可变」的类型，因此可以在不新建字符串的情况下实现原地修改。   
- 剑指 Offer 58 - II. 左旋转字符串
  - 利用切片 `：`
  - 利用列表遍历拼接
  ```class Solution:
    def reverseLeftWords(self, s: str, n: int) -> str:
        res = []
        for i in range(n, n + len(s)):
            res.append(s[i % len(s)])
        return ''.join(res)
      #语法： ‘delimiter’.join(seq)
      #delimiter：分隔符。可以为空
      #delimiter：要连接的元素序列、字符串、元组、字典
  ```
  - 字符串遍历拼接
  ```
  class Solution:
    def reverseLeftWords(self, s: str, n: int) -> str:
        res = ""
        for i in range(n, n + len(s)):
            res += s[i % len(s)]
        return res      
  ```
  
  ### 第4天2022/7/12
  - 剑指 Offer 03. 数组中重复的数字
    - 哈希表 / Set
    - 原地交换
    `Python 中， a, b = c, da,b=c,d 操作的原理是先暂存元组 (c, d)(c,d) ，然后 “按左右顺序” 赋值给 a 和 b 。`
  - 剑指 Offer 53 - I. 在排序数组中查找数字 I
    - 二分法.有优化代码方法。本质是找插入点。 
  - 剑指 Offer 53 - II. 0～n-1中缺失的数字
    - 暴力解法。注意如果是缺少最后一位特殊情况。
    - 二分法.**二分法迷糊点，等号的有无，边界判断**
  
  ### 第5天2022/7/13
  - 剑指 Offer 04. 二维数组中的查找
    - 自己的方法，代码比较麻烦
    ```
    class Solution:
    def findNumberIn2DArray(self, matrix: List[List[int]], target: int) -> bool:
        if len(matrix) == 0:
            return False
        if len(matrix) < len(matrix[0]):
            n, m = len(matrix), len(matrix[0])
        else:
            m, n = len(matrix), len(matrix[0])
        for i in range(n):
            if matrix[i][i] >= target or i == len(matrix)-1 or i ==len(matrix[0])-1:
                for j in range(i, len(matrix)):
                    if matrix[j][0] > target:
                        break
                    for k in range(i+1):
                        if matrix[j][k] > target:
                            break
                        if matrix[j][k] == target:
                            return True
                for j in range(i, len(matrix[0])):
                    if matrix[0][j] > target:
                        break
                    for k in range(i+1):
                        if matrix[k][j] > target:
                            break
                        if matrix[k][j] == target:
                            return True   
                break 
        return False                
    ```
    - 二叉搜索树
    ```
    class Solution:
    def findNumberIn2DArray(self, matrix: List[List[int]], target: int) -> bool:
        i, j = len(matrix) - 1, 0
        while i >= 0 and j < len(matrix[0]):
            if matrix[i][j] > target: i -= 1
            elif matrix[i][j] < target: j += 1
            else: return True
        return False
    ```
  - 剑指 Offer 11. 旋转数组的最小数字
    - 自己的暴力解法
    ```
    class Solution:
    def minArray(self, numbers: List[int]) -> int:
        for i in range(1, len(numbers)):
            if numbers[i-1] > numbers[i]:
                return numbers[i]
        return numbers[0]
    ```
    - 二分法。很难想。事后还需二刷
    ```
    class Solution:
    def minArray(self, numbers: [int]) -> int:
        i, j = 0, len(numbers) - 1
        while i < j:
            m = (i + j) // 2
            if numbers[m] > numbers[j]: i = m + 1
            elif numbers[m] < numbers[j]: j = m
            else: return min(numbers[i:j])
        return numbers[i]
    ```
  - 剑指 Offer 50. 第一个只出现一次的字符
    - 自己的方法，都是hashmap。Python 3.6 后，默认字典就是有序的，因此无需使用 OrderedDict()
      ```
      class Solution:
      def firstUniqChar(self, s: str) -> str:
          dic = {}
          for chr in s:
              if chr in dic:
                  dic[chr] += 1
              else:
                  dic[chr] = 1
          for key, value in dic.items():
              if value == 1:
                  return key
          return ' '
      ```

# Reference
1.[Github文档](https://docs.github.com/cn/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
