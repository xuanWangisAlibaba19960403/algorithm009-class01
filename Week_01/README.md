https://leetcode-cn.com/problems/two-sum/
首先想到的第一个方法也就是最笨的方法
暴力法
时间O(n2) 空间O(1);
##
for (let i = 0; i < nums.length; i++) {
  let j = i + 1;
  避免了重复使用数组中的元素
  for (let j = i + 1; i < nums.length; j++) {
    if (nums[j] = target - nums[i]) {
      return [i, j];
    }
  }
}
##

哈希两次遍历法
时间O(n) 空间O(n);
var twoSum = function(nums, target) {
    // 两次哈希
    const map = new Map();
    const len = nums.length;
    // 把所有的元素放入哈希表中
    for (let i = 0; i < len; i++) {
        map.set(nums[i], i);
    }
    for (let i = 0; i < len; i++) {
        const cur = target - nums[i];
        是否存在并且没有重复使用
        if (map.has(cur) && map.get(cur) != i) {
            return [i, map.get(cur)]
        }
    }
};

哈希一次遍历法
时间O(n) 空间O(n);

var twoSum = function(nums, target) {
    const map = new Map();
    for (let i = 0; i < nums.length; i++) {
        const cur = target - nums[i];
        通过减法式子省去了判断重复使用
        if (map.has(cur)) {
            return [map.get(cur), i]
        }
        map.set(nums[i], i);
    }
};

https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/
没有想到解决的方案
双指针法
var removeDuplicates = function(nums) {
    let i = 0;
    for (let j = 1; j < nums.length; j++) {
        if (nums[i] !== nums[j]) {
            i++;
            // 后面的往前推，达到原地排序的效果
            nums[i] = nums[j];
        }
    }
    // length = i + 1;
    return i + 1;
};
时间O(n2) 空间O(1);

https://leetcode-cn.com/problems/rotate-array/submissions/
暴力法，每次移动一位
var rotate = function (nums, k) {
  if (nums.length < 2 || k === 0) return nums;
  const len = nums.length;
  let temp, previous;
  for (let i = 0; i < k; i++) {
    previous = nums[len - 1];
    for (let j = 0; j < len; j++) {
      const temp = nums[j];
      nums[j] = previous;
      previous = temp;
    }
  }
};
时间O(n*k) 空间O(1);
