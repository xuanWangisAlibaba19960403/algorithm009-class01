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
  k = k % len; // k > len 时只用移动k % len 次即可
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

使用环状替换
求出当前元素最后位置进行替换，保留被替换元素值与索引，为下次替换，通过计数跳出循环
var rotate = function (nums, k) {
  if (nums.length < 2 || k === 0) return nums;
  const len = nums.length;
  k = k % len; // k > len 时只用移动k % len次即可
  let count = 0;
  for (let start = 0; count < len; start++) {
    let current = start;
    let prev = nums[start];
    do {
      const next = (current + k) % len;
      const temp = nums[next];
      nums[next] = prev;
      prev = temp;
      current = next; 
      count++;
    } while (start != current);
  }
}
时间O(n) 空间O(1);

var rotate = function (nums, k) {
  if (nums.length < 2 || k === 0) return nums;
  const len = nums.length;
  k = k % len;
  reverse(nums, 0, len - 1);
  reverse(nums, 0, k - 1);
  reverse(nums, k, len - 1);
}

var reverse = function(nums, start, end) {
  const len = (end - start) // 计算执行次数
  for (let i = 0; i < len; i++) {
    [nums[i + start], nums[end - i]] = [nums[end - i], nums[i + start]];
  }
}
时间O(n) 空间O(1);

https://leetcode-cn.com/problems/merge-two-sorted-lists/submissions/
当l1链表和l2链表都存在时，返回当前值小的节点，通过哨兵，返回正确的链表
var mergeTwoLists = function(l1, l2) {
  if (l1 === null && l2 === null) {
    return null;
  } else if (l1 === null) {
    return l2;
  } else if (l2 === null) {
    return l1;
  }
  const thead = new ListNode(-1);
  let prev = thead;
  while (l1 && l2) {
    if (l1.val < l2.val) {
      prev.next = l1;
      l1 = l1.next;
    } else {
      prev.next = l2;
      l2 = l2.next;
    }
    prev = prev.next;
  }
  prev.next = l1 === null ? l2 : l1;
  return thead.next;
};
时间O(n), 空间O(n)

var mergeTwoLists = function(l1, l2) {
  // 1.终止条件
  // 2.返回值
  if (l1 === null) {
    return l2;
  }
  if (l2 === null) {
    return l1;
  }
  if (l1.val < l2.val) {
    l1.next = mergeTwoLists(l1.next, l2);
    return l1;
  } else {
    l2.next = mergeTwoLists(l1, l2.next);
    return l2;
  }
}
时间O(m + n), 空间O(m + n)

https://leetcode-cn.com/problems/plus-one/
var plusOne = function(digits) {
  if (digits.length === 0) {
    return [];
  }
  const len = digits.length - 1;
  let n = 1;
  for (let i = len; i >= 0; i--) {
    const sum = n + digits[i];
    if (sum >= 10) {
      digits[i] = 0
      n = 1;
    } else {
      digits[i] = sum;
      n = 0;
    }
  }
  if (n >= 1) digits.unshift(n);
  return digits;
};
时间O(n) 空间O(1)

var plusOne = function(digits) {
  if (digits.length === 0) {
    return [];
  }
  const len = digits.length - 1;
  let n = 1;
  for (let i = len; i >= 0; i--) {
    const sum = n + digits[i];
    if (sum >= 10) {
      digits[i] = 0
      n = 1;
    } else {
      // 如果末位不进位 就可以中断了
      digits[i] = sum;
      return digits;
    }
  }
  // 最后一次n=1说明数组需要在最前面补一位0
  if (n >= 1) digits.unshift(n);
  return digits;
};
时间O(n) 空间O(1)

https://leetcode-cn.com/problems/merge-sorted-array/
因为数组为有序数组，所以当前有效索引的元素的值远如果小与另一个有序数组的最大索引元素，那这个元素即为两个数组中最大元素，反之一样
var merge = function (nums1, m, nums2, n) {
  let len = nums1.length - 1;
  m -= 1;
  n -= 1;
  while (n >= 0) {
    if (nums1[m] > nums2[n]) {
      nums1[len] = nums1[m]
      m--;
    } else {
      nums1[len] = nums2[n]
      n--;
    }
    len --;
  }
  return nums1;
}
时间O(n) 空间O(1)

https://leetcode-cn.com/problems/move-zeroes/submissions/
var moveZeroes = function(nums) {
  if (nums.length < 2) {
    return;
  }
  let j = 0;
  const len = nums.length;
  for (let i = 0; i < len; i++) {
    if (nums[i] !== 0) {
      nums[j++] = nums[i];
    }
  }
  for (let i = j; i < len; i++) {
    nums[i] = 0;
  }
};
时间O(n) 空间O(1)

var moveZeroes = function(nums) {
  if (nums.length < 2) {
    return;
  }
  let j = 0;
  const len = nums.length;
  for (let i = 0; i < len; i++) {
    if (nums[i] !== 0) { // 第一个数为非0时候 有一次额外操作
      const temp = nums[i];
      nums[i] = nums[j];
      nums[j++] = temp;
    }
  }
};
时间O(n) 空间O(1)

var moveZeroes = function(nums) {
  if (nums.length < 2) {
    return;
  }
  let j = 0;
  const len = nums.length;
  for (let i = 0; i < len; i++) {
    if (nums[i] !== 0) {
      if (i > j) { // 避免双指针指向同一个元素 做额外操作
        nums[j] = nums[i];
        nums[i] = 0;
      }
      j ++;
    }
  }
};
