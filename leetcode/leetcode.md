### LeetCode 笔记

#### 数据结构基础

##### 1. 数组 （Array）

###### 136.  只出现一次的数字

```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        d = dict()
        for i in range(len(nums)):
            if nums[i] in d :
                d[nums[i]] += 1
            else:
                d[nums[i]] = 1 
        for i in d.items():
            if i[1] == 1:
                return int(i[0])
```

###### 169.  多数元素

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        hashtable = dict()
        # res = []
        for i,num in enumerate(nums):
            if num in hashtable:
                hashtable[num] += 1 
                if hashtable[num] > len(nums)/2:
                    return num
            else:
                hashtable[num] = 1    
        return num
```

###### 15.  三数之和

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        n = len(nums)
        if (not nums or n<3):
            return []
        nums.sort() # 双指针试用的条件为，排序后的数组
        res = []
        for i in range(n):
            # 如果数组第一个数大于0，则最终结果肯定无法等于0
            if (nums[i]>0): 
                return res
            # 确保i是第一个数,判断相邻两数是否相等
            if (i>0) and nums[i] == nums[i-1]: 
                continue
            L = i +1
            R = n - 1
            while (L<R):
                if (nums[i]+nums[L]+nums[R]==0):
                    res.append([nums[i],nums[L],nums[R]])
                    # 因为nums已经经过排序，所以此时要排除的是L，R指向的相同数字
                    while (L < R and nums[L] == nums[L + 1]):
                        L = L + 1
                    while (L < R and nums[R] == nums[R - 1]):
                        R = R - 1
                    L += 1
                    R -= 1
                elif (nums[i]+nums[L]+nums[R]>0):
                    R -= 1
                elif (nums[i]+nums[L]+nums[R]<0):
                    L += 1
        return res
```

###### 75.  颜色分类

```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        for j in range(n):
            i = 0
            while i < n-1:
                if nums[i] > nums[i+1]:
                    nums[i],nums[i+1] = nums[i+1],nums[i]
                i += 1
        return nums
```

###### 56.  合并区间

```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        if not intervals: return []
        intervals.sort()
        res = [intervals[0]]
        for x, y in intervals[1:]:
            if res[-1][1] < x:
                res.append([x, y])
            else:
                res[-1][1] = max(y, res[-1][1])
        return res
```

###### 706.  设计哈希映射

```python
class MyHashMap:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.map = [[-1]*1000 for _ in range(1001)]

    def put(self, key: int, value: int) -> None:
        """
        value will always be non-negative.
        """
        row,col = key//1000,key%1000 
        self.map[row][col] = value


    def get(self, key: int) -> int:
        """
        Returns the value to which the specified key is mapped, or -1 if this map contains no mapping for the key
        """
        row,col = key//1000,key%1000 
        return self.map[row][col]


    def remove(self, key: int) -> None:
        """
        Removes the mapping of the specified value key if this map contains a mapping for the key
        """
        row,col = key//1000,key%1000 
        self.map[row][col] = -1
```

###### 119.  杨辉三角 III

```python
class Solution:
    def getRow(self, rowIndex: int) -> List[int]:
        res = [[1 for j in range(i+1)] for i in range(rowIndex+1)]
        for i in range(2,rowIndex+1):
            for j in range(1,i):
                res[i][j] = res[i-1][j-1]+res[i-1][j]
        return res[-1]
```

###### 48.  旋转图像

```python
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        n = len(matrix)
        # 水平换
        for i in range(n//2):
            for j in range(n):
                matrix[i][j],matrix[n-i-1][j] = matrix[n-i-1][j],matrix[i][j]
        #对角换
        for i in range(n):
            for j in range(i):
                matrix[i][j],matrix[j][i] = matrix[j][i],matrix[i][j]
```

###### 59.  螺旋矩阵 II

```python
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        matrix = [[1 for j in range(n)] for _ in range(n)]
        l,r = 0,n-1
        t,b = 0,n-1
        num, tar = 1,n*n
        while num <= tar:
            # l -> r
            for i in range(l,r+1):
                matrix[t][i] = num
                num += 1
            t += 1
            # t -> b
            for i in range(t,b+1):
                matrix[i][r] = num
                num += 1
            r -= 1
            # r -> l
            for i in range(r,l-1,-1):
                matrix[b][i] = num
                num += 1
            b -= 1
            #b -> t
            for i in range(b,t-1,-1):
                matrix[i][l] = num
                num+=1
            l += 1
        return matrix
```

###### 240.  搜索二维矩阵 II

###### 435.  无重叠区间

###### 334.  递增的三元子序列

```python
class Solution:
    def increasingTriplet(self, nums: List[int]) -> bool:
        one,two = float("inf"),float("inf")
        for three in nums:
            if three > two:
                return True 
            elif three <=one:
                one = three
            else:
                two = three 
        return False
```

###### 238.  除自身以外数组的乘积

###### 260.  和为K的子数组

##### 2. 字符串（string）

###### 415.  字符串相加

###### 409.  最长回文串

###### 290.  单词规律

###### 763.  划分字母区间

###### 49.  字母异位词分组

###### 43.  字符串相乘

###### 187.  重复的DNA序列

###### 5.  最长回文子串

##### 3. 链表（Linked List）

###### 2.  两数相加

###### 142.  环形链表 II

###### 160.  相交链表

###### 82.  删除排序链表中的重复元素 II

###### 24.  两两交换链表中的节点

###### 707.  设计链表

###### 25.K个一组翻转链表

###### 143.  重排链表

##### 4. 栈 / 队列（Stack / Queue ）

###### 155.  最小栈

###### 1249.  移除无效的括号

###### 1823.  找出游戏的获胜者

##### 5. 树（Tree）

###### 108.  将有序数组转化为二叉搜索树

###### 105.  从前序和终须遍历序列构造二叉树

###### 103.  二叉树的锯齿形层序遍历





#### 算法入门

##### 1. 二分查找

###### 704.  二分查找

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        l,r = 0,len(nums)-1
        while l <= r:
            m = l + (r-l)//2
            if target == nums[m]:
                return m 
            elif target < nums[m]:
                r = m - 1
            elif target > nums[m]:
                l = m + 1
        return -1
```

###### 278.  第一个错误的的版本

```python
# The isBadVersion API is already defined for you.
# @param version, an integer
# @return an integer
# def isBadVersion(version):

class Solution:
    def firstBadVersion(self, n):
        """
        :type n: int
        :rtype: int
        """
        l,r = 1,n
        while l <= r:
            m = l + (r-l)//2
            if isBadVersion(m):
                r = m -1 
            else:
                l = m + 1 
        return l
```

###### 35.  搜索插入的位置

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        l,r = 0,len(nums)-1
        while l <= r:
            mid = l + (r-l)//2
            if nums[mid] == target:
                return mid 
            if nums[mid] > target:
                r = mid -1
            else:
                l = mid + 1 
        return l
```

##### 2. 双指针

###### 977.  有序数组的平方

###### ==189.  旋转数组==

###### 283.  移动零

###### 167.  两数之和 II

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        l,r = 0,len(numbers)-1
        while l < r:
            if numbers[l]+numbers[r] == target:
                return [l+1,r+1]
            if numbers[l]+numbers[r] < target:
                l += 1
            if numbers[l] + numbers[r] > target:
                r -= 1
        return -1
```

###### 344.  反转字符串

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        l,r = 0,len(s)-1
        while l<r:
            s[l],s[r]=s[r],s[l]
            l+=1
            r-=1
```

###### 557.  反转字符串中的单词 III

###### 876.  链表的中间节点

###### 19.  删除链表的倒数第N个节点

#####  3. 滑动窗口

###### 3.  无重复字符串的最长子串

###### 567.  字符串的排列

```python
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        counter1 = self.getCounter(s1)
        t,n = len(s1),len(s2) 
        i = 0 
        while i < (n-t+1):
            counter2 = self.getCounter(s2[i:i+t])
            if counter1 == counter2:
                return True 
            i += 1 
        return False
    def getCounter(self,strs):
        """
        用于统计字符的个数合种类
        """
        d = dict()
        for s in strs:
            if s in d:
                d[s] += 1
            else:
                d[s] = 1
        return d
```

### 剑指Offer



### 牛客网

#### 牛客网输入输出

https://ac.nowcoder.com/acm/contest/5652/B

https://ac.nowcoder.com/acm/contest/5657#question

https://ac.nowcoder.com/acm/contest/5652#question

#### 牛客网 SQL







