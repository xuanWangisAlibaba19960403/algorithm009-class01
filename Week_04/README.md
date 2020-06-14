使用二分查找，寻找一个半有序数组 [4, 5, 6, 7, 0, 1, 2] 中间无序的地方
说明：同学们可以将自己的思路、代码写在第 4 周的学习总结中

```javascript
        /**
         * @param {number[]} nums
         * @return {number}
        */
        var findSort = function (nums) {
            if (nums.length === 0) {
                return - 1;
            }
            let left = 0, right = nums.length - 1;
            while (left <= right) {
                const mid = (left + right) >> 1;
                if (nums[mid] >= nums[left] && nums[mid] <= nums[right]) {
                    return -1;
                    // 不包含重复的情况下
                    // 如果mid <= left 说明左侧无序
                } else if (nums[mid] <= nums[left]) {
                    return [left, mid];
                    // 如果mid >= rigth 说明右侧无序
                } else if (nums[right] <= nums[mid]) {
                    return [mid + 1, right];
                }
            }
        }
```

## 第10课 贪心

每一步选择中都选择当前状态下最好的，从而希望导致全局结果是最优的。

贪心法也可以用作辅助算法或者直接解决一些要求结果不特别精确的问题。

### 适用贪心算法的场景

简单地说，问题能够分解成子问题来解决，子问题的最优解能递推到最终问题的最优解。这种子问题最优解称为最优子结构。

贪心算法与动态规划的不同在于它对每个子问题的解决方案都做出选择，不能回退。动态规划则会保存以前的运算结果，并根据以前的结果对当前进行选择，有回退功能。

## 第11课 二分查找

```
# Python
left, right = 0, len(array) - 1 
while left <= right: 
	  mid = (left + right) / 2 
	  if array[mid] == target: 
		    # find the target!! 
		    break or return result 
	  elif array[mid] < target: 
		    left = mid + 1 
	  else: 
		    right = mid - 1
```