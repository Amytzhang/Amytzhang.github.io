<template><div><h1 id="archive-article1" tabindex="-1"><a class="header-anchor" href="#archive-article1"><span>Archive Article1</span></a></h1>
<h1 id="heading-1" tabindex="-1"><a class="header-anchor" href="#heading-1"><span>Heading 1</span></a></h1>
<h1 id="力扣小结-双指针" tabindex="-1"><a class="header-anchor" href="#力扣小结-双指针"><span>力扣小结：双指针</span></a></h1>
<p>双指针是一种常用的解题技巧，通常用于解决数组或链表相关的问题。下面是一些解题思路或步骤：</p>
<ol>
<li>快慢指针：快慢指针通常用于解决链表中的问题，比如判断链表是否有环、找到链表的中间节点等。快指针每次移动两步，慢指针每次移动一步，通过比较快慢指针的位置来解决问题。</li>
<li>左右指针：左右指针通常用于解决数组或字符串中的问题，比如找到两数之和、反转字符串等。左指针从数组的起始位置开始，右指针从数组的末尾开始，根据问题的要求移动左右指针来解决问题。</li>
<li>滑动窗口：滑动窗口是一种特殊的双指针技巧，通常用于解决子数组或子字符串相关的问题，比如找到最小子数组的和、找到字符串中的最长无重复字符子串等。滑动窗口的思路是维护一个窗口，通过移动左右指针来调整窗口的大小，从而解决问题。
双指针法则：在解决问题时，可以根据问题的要求选择合适的双指针技巧，然后根据问题的特点设计合适的移动规则，最后根据移动规则编写代码实现解题思路。</li>
</ol>
<h1 id="_1、快慢指针" tabindex="-1"><a class="header-anchor" href="#_1、快慢指针"><span>1、快慢指针</span></a></h1>
<h2 id="_283" tabindex="-1"><a class="header-anchor" href="#_283"><span>283</span></a></h2>
<div class="language-text line-numbers-mode" data-highlighter="prismjs" data-ext="text" data-title="text"><pre v-pre><code><span class="line"></span>
<span class="line">/**</span>
<span class="line"></span>
<span class="line">* @param {number[]} nums</span>
<span class="line">* @return {void} Do not return anything, modify nums in-place instead.</span>
<span class="line">*/</span>
<span class="line">var moveZeroes = function(nums) {</span>
<span class="line">    let low = 0,fast=0;</span>
<span class="line">    while(fast&lt;nums.length) {</span>
<span class="line">      if(nums[fast]!=0) {</span>
<span class="line">        changeTanslate(nums,low,fast)</span>
<span class="line">        low++</span>
<span class="line">      }</span>
<span class="line">      fast++</span>
<span class="line">     }</span>
<span class="line">    };</span>
<span class="line">    function changeTanslate(nums,start,end) {</span>
<span class="line">      let temp = nums[start]</span>
<span class="line">      nums[start] = nums[end]</span>
<span class="line">      nums[end] = temp</span>
<span class="line">    }</span>
<span class="line"></span>
<span class="line"></span></code></pre>
<div class="line-numbers" aria-hidden="true" style="counter-reset:line-number 0"><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div></div></div><h1 id="_2、左右指针" tabindex="-1"><a class="header-anchor" href="#_2、左右指针"><span>2、左右指针</span></a></h1>
<h2 id="_42、11" tabindex="-1"><a class="header-anchor" href="#_42、11"><span>42、11</span></a></h2>
<div class="language-text line-numbers-mode" data-highlighter="prismjs" data-ext="text" data-title="text"><pre v-pre><code><span class="line"></span>
<span class="line">var trap = function(height) {</span>
<span class="line">    let ans = 0;</span>
<span class="line">    let left = 0, right = height.length - 1;</span>
<span class="line">    let leftMax = 0, rightMax = 0;</span>
<span class="line">    while (left &lt; right) {</span>
<span class="line">        leftMax = Math.max(leftMax, height[left]);</span>
<span class="line">        rightMax = Math.max(rightMax, height[right]);</span>
<span class="line">        if (height[left] &lt; height[right]) {</span>
<span class="line">            ans += leftMax - height[left];</span>
<span class="line">            ++left;</span>
<span class="line">        } else {</span>
<span class="line">            ans += rightMax - height[right];</span>
<span class="line">            --right;</span>
<span class="line">        }</span>
<span class="line">    }</span>
<span class="line">    return ans;</span>
<span class="line">};</span>
<span class="line"></span>
<span class="line"></span></code></pre>
<div class="line-numbers" aria-hidden="true" style="counter-reset:line-number 0"><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div></div></div><div class="language-text line-numbers-mode" data-highlighter="prismjs" data-ext="text" data-title="text"><pre v-pre><code><span class="line"></span>
<span class="line">/**</span>
<span class="line"></span>
<span class="line">* @param {number[]} height</span>
<span class="line">* @return {number}</span>
<span class="line">*/</span>
<span class="line">const maxArea = height => {</span>
<span class="line">// 定义两个指针，分别指向头尾</span>
<span class="line">let [m, n] = [0, height.length - 1]; // 定义最大区域 let maxArea = 0; // 若m=n，则面积为0，所以不取等于</span>
<span class="line">while (m &lt; n) { // 当前有效面积的高</span>
<span class="line">const h = Math.min(height[m], height[n]); // 当前面积 const area = (n - m)* h; // 更新最大面积</span>
<span class="line">maxArea = Math.max(maxArea, area); // 更新指针</span>
<span class="line">if (height[m] &lt; height[n]) {</span>
<span class="line">// 左指针对应的值小，左指针右移</span>
<span class="line">m++;</span>
<span class="line">} else {</span>
<span class="line">// 右指针对应的值小，右指针左移</span>
<span class="line">n--;</span>
<span class="line">}</span>
<span class="line">}</span>
<span class="line">return maxArea;</span>
<span class="line">};</span>
<span class="line"></span>
<span class="line"></span></code></pre>
<div class="line-numbers" aria-hidden="true" style="counter-reset:line-number 0"><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div><div class="line-number"></div></div></div></div></template>


