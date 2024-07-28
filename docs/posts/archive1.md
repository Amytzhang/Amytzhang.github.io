---
date: 2024-7-20
category:
  - History
tag:
  - vue3设计原理
archive: true
---

# Archive Article1

# Heading 1

# 力扣小结：双指针

双指针是一种常用的解题技巧，通常用于解决数组或链表相关的问题。下面是一些解题思路或步骤：

1. 快慢指针：快慢指针通常用于解决链表中的问题，比如判断链表是否有环、找到链表的中间节点等。快指针每次移动两步，慢指针每次移动一步，通过比较快慢指针的位置来解决问题。
2. 左右指针：左右指针通常用于解决数组或字符串中的问题，比如找到两数之和、反转字符串等。左指针从数组的起始位置开始，右指针从数组的末尾开始，根据问题的要求移动左右指针来解决问题。
3. 滑动窗口：滑动窗口是一种特殊的双指针技巧，通常用于解决子数组或子字符串相关的问题，比如找到最小子数组的和、找到字符串中的最长无重复字符子串等。滑动窗口的思路是维护一个窗口，通过移动左右指针来调整窗口的大小，从而解决问题。
 双指针法则：在解决问题时，可以根据问题的要求选择合适的双指针技巧，然后根据问题的特点设计合适的移动规则，最后根据移动规则编写代码实现解题思路。

# 1、快慢指针

## 283

```

/**

* @param {number[]} nums
* @return {void} Do not return anything, modify nums in-place instead.
*/
var moveZeroes = function(nums) {
    let low = 0,fast=0;
    while(fast<nums.length) {
      if(nums[fast]!=0) {
        changeTanslate(nums,low,fast)
        low++
      }
      fast++
     }
    };
    function changeTanslate(nums,start,end) {
      let temp = nums[start]
      nums[start] = nums[end]
      nums[end] = temp
    }

```

# 2、左右指针

## 42、11

```

var trap = function(height) {
    let ans = 0;
    let left = 0, right = height.length - 1;
    let leftMax = 0, rightMax = 0;
    while (left < right) {
        leftMax = Math.max(leftMax, height[left]);
        rightMax = Math.max(rightMax, height[right]);
        if (height[left] < height[right]) {
            ans += leftMax - height[left];
            ++left;
        } else {
            ans += rightMax - height[right];
            --right;
        }
    }
    return ans;
};

```

```

/**

* @param {number[]} height
* @return {number}
*/
const maxArea = height => {
// 定义两个指针，分别指向头尾
let [m, n] = [0, height.length - 1]; // 定义最大区域 let maxArea = 0; // 若m=n，则面积为0，所以不取等于
while (m < n) { // 当前有效面积的高
const h = Math.min(height[m], height[n]); // 当前面积 const area = (n - m)* h; // 更新最大面积
maxArea = Math.max(maxArea, area); // 更新指针
if (height[m] < height[n]) {
// 左指针对应的值小，左指针右移
m++;
} else {
// 右指针对应的值小，右指针左移
n--;
}
}
return maxArea;
};

```
