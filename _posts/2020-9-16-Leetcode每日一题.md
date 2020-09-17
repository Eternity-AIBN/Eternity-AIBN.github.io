# Leetcode 每日一题

[TOC]



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

   ==TODO==

4. 思考 / 学到啥

   ==TODO==





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