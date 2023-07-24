---
title: Leetcode随缘刷题
date: 2020-09-16 00:00:00 +0800
categories: [Data structure and algorithm, Leetcode]
tags: [leetcode]     # TAG names should always be lowercase
---


#### [239. 滑动窗口最大值](https://leetcode-cn.com/problems/sliding-window-maximum/) 2020-9-16

##### 题目描述

给定一个数组 nums，有一个大小为 k 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 k 个数字。滑动窗口每次只向右移动一位。返回滑动窗口中的最大值。

**进阶：**你能在线时间复杂度内解决此题吗？

**示例：**

> 输入: nums = [1,3,-1,-3,5,3,6,7], 和 k = 3
> 输出: [3,3,5,5,6,7] 
> 解释: 
>
>   滑动窗口的位置                最大值
> ---------------               -----
> [1  3  -1] -3  5  3  6  7       		3
>  1 [3  -1  -3] 5  3  6  7       		3
>  1  3 [-1  -3  5] 3  6  7      		 5
>  1  3  -1 [-3  5  3] 6  7      		 5
>  1  3  -1  -3 [5  3  6] 7       		6
>  1  3  -1  -3  5 [3  6  7]      		7

**提示：**

- `1 <= nums.length <= 10^5`
- `-10^4 <= nums[i] <= 10^4`
- `1 <= k <= nums.length`



##### 解法

1. 暴力法：两层`for`循环

2. 线性时间解法：类似于维护一个`单调栈`，每次比较当前元素`num[i]`与栈顶元素大小，若前者大则则栈顶弹出，直至栈为空或者栈顶大于`num[i]`时，将`num[i]`入栈，如此栈底元素即为当前窗口最大值。此外由于滑动窗口大小有限，当上一次的最大值从窗口中滑出时，需要将其从栈中删去（故而未使用`Stack`，而是用`Vector`模拟栈），因此也需记载下栈顶元素下标（采用`pair<int,int>`，`first`表示元素值，`second`表示下标）。

   ```C++
   vector<int> maxSlidingWindow(vector<int>& nums, int k) {
   	vector<int> ans;
   	vector<pair<int,int>> stack;
   	int size = 0;
   	int i = 0;
   	for (; i < nums.size(); ++i) {
   		if (!stack.empty() && i - stack.front().second >= k) {   //最大元素已不在窗口中，将其删去
   			stack.erase(stack.begin());
   		}
   		if (stack.empty()) {
   			stack.push_back(pair<int, int>(nums[i], i));
   		}
   		else {
   			pair<int, int> last = stack.back();
   			while (nums[i] >= last.first) {
   				stack.pop_back();
   				if (stack.empty()) {
   					break;
   				}
   				last = stack.back();
   			}
   			stack.push_back(pair<int, int>(nums[i], i));
   		}
   		if (i >= k - 1)
   			ans.push_back(stack.front().first);
   	}
   
   	return ans;
   }
   ```

3. 进一步优化 / 大佬解法

   __TODO__

4. 思考 / 学到啥

   __TODO__





#### [76. 最小覆盖子串](https://leetcode-cn.com/problems/minimum-window-substring/) 2020-9-17

##### 题目描述

给你一个字符串 S、一个字符串 T 。请你设计一种算法，可以在 O(n) 的时间复杂度内，从字符串 S 里面找出：包含 T 所有字符的最小子串。

**示例：**

> 输入：S = "ADOBECODEBANC", T = "ABC"
> 输出："BANC"

**提示：**

- 如果 S 中不存这样的子串，则返回空字符串 `""`。
- 如果 S 中存在这样的子串，我们保证它是唯一的答案。



##### 解法

1. 





#### [8. 字符串转换整数 (atoi)](https://leetcode-cn.com/problems/string-to-integer-atoi) 2020-12-2





#### [324. 摆动排序 II](https://leetcode-cn.com/problems/wiggle-sort-ii/) 2020-12-2



1. 排序 + 插入，注意应该是__倒插！！！__

   为何？比如：$a≤b≤c≤d$，正常处理为：$a,c,b,d$，b和c在一块，可能出现问题；若倒插，则为$b,d,a,c$，中间两个数为a和d，差距比b和c大，不会出现问题。

2. 更好的解法：快排partition的应用......竟然没想到





#### [91. 解码方法](https://leetcode-cn.com/problems/decode-ways/) 2020-12-3





#### [233. 数字 1 的个数](https://leetcode-cn.com/problems/number-of-digit-one/) 2020-12-7

糊里糊涂一点点硬编码，超过100%.....
<img src="C:\Users\15542\AppData\Roaming\Typora\typora-user-images\image-20201207205745217.png" alt="image-20201207205745217" style="zoom:50%;" />

主要思路：分位数计算，比如输入12345，依次计算0 ~ 10000、0 ~ 1000、0 ~ 100、0 ~ 10的结果，需要注意的是，在计算0 ~ 10000时，还需加上2345+1（10000及以上有2345+1个数，会带有“10000”的“1”）



#### [50. Pow(x, n)](https://leetcode-cn.com/problems/powx-n/) 2020-12-8

直接循环n次会超时，考虑到一直是乘以同一个数（$x^n=x*x*x*x...$），可以这样计算：$x^n=x^{\frac{1}{2}}*x^{\frac{1}{2}}=...$，将复杂度从$O(n)$降为$O(log_2n)$



#### [84. 柱状图中最大的矩形](https://leetcode-cn.com/problems/largest-rectangle-in-histogram/) 2020-12-9

暴力法：依次遍历每个元素heights[i]，以heights[i]为矩形高度，分别向前、后扩张宽度，每次可得一个矩形，计算其面积，比较取最大值即可。

```c++
int largestRectangleArea(vector<int>& heights) {
	int size = heights.size();
	int ans = 0;
	int curHeight, len;
	for (int i = 0; i < size; ++i) {
		len = 1;
		curHeight = heights[i];
		int tmp = i;
		while (tmp > 0 && heights[tmp - 1] >= curHeight) {
			tmp--;
			len++;
		}
		tmp = i;
		while (tmp < size-1 && heights[tmp + 1] >= curHeight) {
			tmp++;
			len++;
		}
		tmp = len*curHeight;
		if (tmp > ans)ans = tmp;
	}
	return ans;
}
```

单调栈：维护一个单调递减栈，栈中存放元素下标，每次弹出元素时计算以其为高的矩形面积，比较取最大值即可。存放下标是为了方便在计算矩形时获取其宽。





#### [315. 计算右侧小于当前元素的个数](https://leetcode-cn.com/problems/count-of-smaller-numbers-after-self/) 2020-12-10

归并排序求逆序对

好像还有其他做法.....





#### [140. 单词拆分 II](https://leetcode-cn.com/problems/word-break-ii/) 2020-12-15







#### [338. 比特位计数](https://leetcode-cn.com/problems/counting-bits/) 2021-3-3

分三种情况：

* i 为偶数，即二进制以 0 结尾（00和10）：因为不存在进位问题，下一个数 1 的数目必然比当前**多一**
* 以 01 结尾：下一个数以 10 结尾，1 的数目**不变**
* 以 11 结尾：下一个数以 00 结尾，此时发生**连续进位**，实际上可看成：aaa11 + 1 = aaa00 + 100，考虑 1 的数目，则相当于 aaa+1，利用动态规划查看`ans[aaa+1]`的结果即为`ans[aaa11]`的结果



#### [907. 子数组的最小值之和](https://leetcode-cn.com/problems/sum-of-subarray-minimums/) 2021-3-4

不可直接求每个子数组的最小值然后求和，会超时！

直接计算每个数作为最小值的次数即可——类似于算法课学过的，用动态规划以避免重复寻找更小的值



#### [300. 最长递增子序列](https://leetcode-cn.com/problems/longest-increasing-subsequence/) 2021-3-4

有多种动态规划的做法：

* 最基础的方法：$O(N^2)$

  `p[i]`表示以第`i`个数字结尾的最长严格递增子序列长度；

  从`p[i]`到`p[i+1]`：只需遍历前`i`个数字，以其结尾的`i`种情况分别是否可以加上`i+1`

* 进阶：

* $O(NlogN)$：https://blog.csdn.net/u012505432/article/details/52228945?utm_medium=distribute.pc_relevant.none-task-blog-baidujs_baidulandingword-0&spm=1001.2101.3001.4242

  

#### [354. 俄罗斯套娃信封问题](https://leetcode-cn.com/problems/russian-doll-envelopes/) 2021-3-4

* 基础法：同上体$O(N^2)$
* 





#### [232. 用栈实现队列](https://leetcode-cn.com/problems/implement-queue-using-stacks/) 2021-3-5

简单题，平摊分析时间复杂度



#### [54. 螺旋矩阵](https://leetcode-cn.com/problems/spiral-matrix/) 2021-3-5

直接模拟旋转过程，注意细节别出错即可



#### [61. 旋转链表](https://leetcode-cn.com/problems/rotate-list/) 2021-3-5

注意移动次数远大于链表长度时，会有多余的移动，应消除以免超时。

可以不用循环模拟k次移动，直接寻找最终头结点即可。



#### [33. 搜索旋转排序数组](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/) 2021-3-5

没想明白。。。

* 主要思想：数组一分为二，必有一部分有序、另一部分可能无序，在有序部分二分查找，无序部分递归该过程。
* 上述方法使用递归导致空间复杂度上升，可不采用递归：直接判断target是否在有序部分中，若是则二分查找，否则将另一部分一分为二重复上述过程。



#### [81. 搜索旋转排序数组 II](https://leetcode-cn.com/problems/search-in-rotated-sorted-array-ii/) 2021-3-5

仍可采用二分查找，但由于重复元素的出现，最坏情况下复杂度不再是$O(logn)$而是$O(n)$。

问题在于通过判断`nums[l]`和`nums[mid]`的大小不再可确定该部分是否有序：如`[1,0,1,1,1]`

中`nums[0]=nums[2]=1`，但该部分实际上不是有序的（因为还存在着`nums[2]=nums[4]`，某种意义上你也可以说“我认为后面部分是有序的”）。那么这种情况如何判断哪部分是有序的呢？——只能遍历其中一部分，若有与`nums[mid]`不同的值，则该部分无序，另一部分有序。



#### [153. 寻找旋转排序数组中的最小值](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/) 2021-3-5

应该在上面两道题之前做的hhh

* 若无序：显然最小值必然出现在无序部分，不断二分即可。

* 若有序：首个元素为最小值



#### [503. 下一个更大元素 II](https://leetcode-cn.com/problems/next-greater-element-ii/) 2021-3-6

简单的单调栈，注意栈中存的是**下标**就行



#### [剑指 Offer 64. 求1+2+…+n](https://leetcode-cn.com/problems/qiu-12n-lcof/) 2021-3-6

* 首先想到递归

  ```c++
  int sumNums(int n) {
     	if(n==1) return 1;
      return n + sumNums(n-1);
  }
  ```

  不能用`if`，想办法替代它：逻辑运算符

  ```c++
  int sumNums(int n) {
     	n&&(n = n+sumNums(n-1));
      return n;
  }
  ```

* 移位实现乘法



#### [剑指 Offer 31. 栈的压入、弹出序列](https://leetcode-cn.com/problems/zhan-de-ya-ru-dan-chu-xu-lie-lcof/) 2021-3-6

* 直接模拟进出栈过程



#### [剑指 Offer 38. 字符串的排列](https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/) 2021-3-6

* 递归：`“abc”`的排列方式即为将`a`插入`"bc"`所有排列方式，至于如何插入——每个位置都可；对于字符串中有重复字符的情况，最后将排列中的重复方式删去即可。

  缺点：时、空间复杂度很大

* 优化：处理重复字符的方式——在递归过程中**剪枝**，而不是放到最后处理

* 再优化：出现重复后去重—>不让重复出现—>自己原来的递归方式不太合适，要修改，利用**set**可避免重复

* [LC大神回溯法](https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/solution/mian-shi-ti-38-zi-fu-chuan-de-pai-lie-hui-su-fa-by/)，实际上是`DFS`



#### [131. 分割回文串](https://leetcode-cn.com/problems/palindrome-partitioning/) 2021-3-7

* 一开始想将字符串一分为二，分别dfs再合并得到一组结果，遍历所有可能的分割位置得到答案，但实际上这样过于复杂，且会有重复计算（比如`abc`，分成`a`和`bc`后得到的结果中已经有`[a,b,c]`，再分成`ab`和`c`时，`ab`不回文，直接放弃这种情况即可，因为如果你对`ab`再递归下去得到的结果只会是重复的）——即无需对左边部分进行递归，只需要**在左边是回文串的情况下递归右半部分即可**
* **回溯不太会啊。。。**

