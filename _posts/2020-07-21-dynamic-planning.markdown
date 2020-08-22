---

layout:     post
title:      "动态规划-自己的一点理解"
subtitle:   " \"Dynamic Programming\""
date:       2020-07-21 15:56:27
author:     "Durant"
latex: true
header-img: "img/post-bg-alitrip.jpg"
catalog: true
tags:
    - 算法

---

> 动态规划(DP)的重要性我就不用说了，`LeetCode` 上DP问题多达228道，仅次于数组301题。

>个人感觉，DP问题就像斐波那契数列一样，你需要找到能够递归的通式子，我们把这个式子称作状态转移方程，没错，就是数电里面那个~ o(*￣▽￣*)o。

然后，现在我们干一件事情，把DP题目罗列出来，找到共同点，未来我们要做到看一眼题目就知道用什么方法。
下面摘至[Huahua's problem set](http://zxi.mytechroad.com/blog/leetcode-problem-categories/?from=singlemessage). 

---

70. [爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/) (Easy)

746. [使用最小花费爬楼梯](https://leetcode-cn.com/problems/min-cost-climbing-stairs/) (Easy)

198. [打家劫舍](https://leetcode-cn.com/problems/house-robber/)(Easy)

64. [最小路径和](https://leetcode-cn.com/problems/minimum-path-sum/)(Medium)

62. [不同路径](https://leetcode-cn.com/problems/unique-paths/)(Medium)

63. [不同路径2](https://leetcode-cn.com/problems/unique-paths-ii/)(Medium)

96.[不同的搜索二叉树](https://leetcode-cn.com/problems/unique-binary-search-trees/)(Medium)

221.[最大正方形](https://leetcode-cn.com/problems/maximal-square/)(medium)

53. [最大字序和](https://leetcode-cn.com/problems/maximum-subarray/solution/zui-da-zi-xu-he-by-leetcode-solution/)(Easy)
    139. [单词拆分(Medium)](https://leetcode-cn.com/problems/word-break/solution/)

152. [乘积最大子数组(Medium)](https://leetcode-cn.com/problems/maximum-product-subarray)

53. [分割数组的最大和](https://leetcode-cn.com/problems/split-array-largest-sum/)(Hard)

10.[正则表达式匹配](https://leetcode-cn.com/problems/regular-expression-matching/)(Hard)

44. [通配符匹配](https://leetcode-cn.com/problems/wildcard-matching/)(Hard)

72 [编辑距离](https://leetcode-cn.com/problems/edit-distance/)(Hard)



<div id="sheets-viewport"> <div dir="ltr" id="1674276502" style=""> <div class="ritz grid-container" dir="ltr"> <table cellpadding="0" cellspacing="0" class="waffle"> <thead> <tr> <th class="row-header freezebar-origin-ltr header-shim row-header-shim"> </th> <th class="header-shim" id="1674276502C0" style="width:36px"> </th> <th class="header-shim" id="1674276502C1" style="width:187px"> </th> <th class="header-shim" id="1674276502C2" style="width:72px"> </th> <th class="header-shim" id="1674276502C3" style="width:50px"> </th> <th class="header-shim" id="1674276502C4" style="width:50px"> </th> <th class="header-shim" id="1674276502C5" style="width:50px"> </th> <th class="header-shim" id="1674276502C6" style="width:50px"> </th> <th class="header-shim" id="1674276502C7" style="width:50px"> </th> <th class="header-shim" id="1674276502C8" style="width:197px"> </th> </tr> </thead> <tbody> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R0" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 1 </div> </th> <td class="s84" dir="ltr"> Id </td> <td class="s85" dir="ltr"> Name </td> <td class="s86" dir="ltr"> Difficulty </td> <td class="s86" colspan="5" dir="ltr"> Similar Problems </td> <td class="s87" dir="ltr"> Comments </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R1" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 2 </div> </th> <td class="s84" dir="ltr"> 70 </td> <td class="s88" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-70-climbing-stairs/"> Climbing Stairs </a> </td> <td class="s86" dir="ltr"> ★ </td> <td class="s89" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-746-min-cost-climbing-stairs/"> 746 </a> </td> <td class="s89" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-1137-n-th-tribonacci-number/"> 1137 </a> </td> <td class="s84"> </td> <td class="s84"> </td> <td class="s84"> </td> <td class="s90" dir="ltr" rowspan="3"> I: O(n), S = O(n), T = O(n) </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R2" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 3 </div> </th> <td class="s84" dir="ltr"> 303 </td> <td class="s88" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-303-range-sum-query-immutable/"> Range Sum Query – Immutable </a> </td> <td class="s86" dir="ltr"> ★ </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-1218-longest-arithmetic-subsequence-of-given-difference/"> 1218 </a> </td> <td class="s84" dir="ltr"> </td> <td class="s84" dir="ltr"> </td> <td class="s84" dir="ltr"> </td> <td class="s84" dir="ltr"> </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R3" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 4 </div> </th> <td class="s84" dir="ltr"> 53 </td> <td class="s88" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-53-maximum-subarray/"> Maximum Subarray </a> </td> <td class="s86" dir="ltr"> ★★ </td> <td class="s89" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-121-best-time-to-buy-and-sell-stock/"> 121 </a> </td> <td class="s84" dir="ltr"> </td> <td class="s84" dir="ltr"> </td> <td class="s84" dir="ltr"> </td> <td class="s84" dir="ltr"> </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R4" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 5 </div> </th> <td class="s92" dir="ltr" rowspan="2"> 62 </td> <td class="s93" dir="ltr" rowspan="2"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-62-unique-paths/"> Unique Paths </a> </td> <td class="s94" dir="ltr" rowspan="2"> ★★ </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-63-unique-paths-ii/"> 63 </a> </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-64-minimum-path-sum/"> 64 </a> </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-120-triangle/"> 120 </a> </td> <td class="s95" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-174-dungeon-game/"> 174 </a> </td> <td class="s95" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-931-minimum-falling-path-sum/"> 931 </a> </td> <td class="s90" dir="ltr" rowspan="3"> I: O(mn), S = O(mn), T = O(mn) </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R5" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 6 </div> </th> <td class="s95" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/searching/leetcode-1210-minimum-moves-to-reach-target-with-rotations/"> 1210 </a> </td> <td class="s84" dir="ltr"> </td> <td class="s84" dir="ltr"> </td> <td class="s84" dir="ltr"> </td> <td class="s84" dir="ltr"> </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R6" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 7 </div> </th> <td class="s84" dir="ltr"> 85 </td> <td class="s88" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-85-maximal-rectangle/"> Maximal Rectangle </a> </td> <td class="s86" dir="ltr"> ★★★ </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-304-range-sum-query-2d-immutable/"> 221 </a> </td> <td class="s89" dir="ltr"> <a href="https://leetcode.com/problems/range-sum-query-2d-immutable"> 304 </a> </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-1277-count-square-submatrices-with-all-ones/"> 1277 </a> </td> <td class="s84"> </td> <td class="s84"> </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R7" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 8 </div> </th> <td class="s84" dir="ltr"> 198 </td> <td class="s88" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-198-house-robber/"> House Robber </a> </td> <td class="s86" dir="ltr"> ★★★ </td> <td class="s91" dir="ltr"> <a href="https://leetcode.com/problems/house-robber-ii/"> 213 </a> </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-309-best-time-to-buy-and-sell-stock-with-cooldown/"> 309 </a> </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-740-delete-and-earn/"> 740 </a> </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-790-domino-and-tromino-tiling/"> 790 </a> </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-801-minimum-swaps-to-make-sequences-increasing/"> 801 </a> </td> <td class="s87" dir="ltr"> I: O(n), S = O(3n), T = O(3n) </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R8" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 9 </div> </th> <td class="s84" dir="ltr"> 279 </td> <td class="s88"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-279-perfect-squares/"> Perfect Squares </a> </td> <td class="s86" dir="ltr"> ★★★ </td> <td class="s87"> </td> <td class="s87"> </td> <td class="s84"> </td> <td class="s84"> </td> <td class="s84"> </td> <td class="s87" dir="ltr"> I: n, S = O(n), T = O(n*sqrt(n)) </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R9" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 10 </div> </th> <td class="s84" dir="ltr"> 139 </td> <td class="s88" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/leetcode/leetcode-139-word-break/"> Word Break </a> </td> <td class="s86" dir="ltr"> ★★★ </td> <td class="s95" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/leetcode/leetcode-140-word-break-ii/"> 140 </a> </td> <td class="s95" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/searching/leetcode-818-race-car/"> 818 </a> </td> <td class="s84"> </td> <td class="s84"> </td> <td class="s84"> </td> <td class="s90" dir="ltr" rowspan="3"> I: O(n), S = O(n), T = O(n^2) </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R10" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 11 </div> </th> <td class="s84" dir="ltr"> 300 </td> <td class="s88" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-300-longest-increasing-subsequence/"> Longest Increasing Subsequence </a> </td> <td class="s86" dir="ltr"> ★★★ </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-673-number-of-longest-increasing-subsequence/"> 673 </a> </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/leetcode/leetcode-weekly-contest-137/"> 1048 </a> </td> <td class="s84" dir="ltr"> </td> <td class="s84"> </td> <td class="s84"> </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R11" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 12 </div> </th> <td class="s84" dir="ltr"> 96 </td> <td class="s88" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-96-unique-binary-search-trees/"> Unique Binary Search Trees </a> </td> <td class="s86" dir="ltr"> ★★★ </td> <td class="s84" dir="ltr"> </td> <td class="s84" dir="ltr"> </td> <td class="s84" dir="ltr"> </td> <td class="s84" dir="ltr"> </td> <td class="s84" dir="ltr"> </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R12" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 13 </div> </th> <td class="s84" dir="ltr"> 1105 </td> <td class="s88" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-1105-filling-bookcase-shelves/"> Filling Bookcase Shelves </a> </td> <td class="s86" dir="ltr"> ★★★ </td> <td class="s84" dir="ltr"> </td> <td class="s84" dir="ltr"> </td> <td class="s84" dir="ltr"> </td> <td class="s84" dir="ltr"> </td> <td class="s84" dir="ltr"> </td> <td class="s96" dir="ltr"> <div class="softmerge-inner" style="width: 295px; left: -1px;"> I: O(n) + t, S = O(n), T = O(n^2) </div> </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R13" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 14 </div> </th> <td class="s84" dir="ltr"> 131 </td> <td class="s88" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/searching/leetcode-131-palindrome-partitioning/"> Palindrome Partitioning </a> </td> <td class="s86" dir="ltr"> ★★★ </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-89-gray-code/"> 89 </a> </td> <td class="s84" dir="ltr"> </td> <td class="s84"> </td> <td class="s84"> </td> <td class="s84"> </td> <td class="s97" dir="ltr"> <div class="softmerge-inner" style="width: 295px; left: -1px;"> I: O(n), S = O(2^n), T = O(2^n) </div> </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R14" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 15 </div> </th> <td class="s92" dir="ltr" rowspan="2"> 72 </td> <td class="s93" dir="ltr" rowspan="2"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-72-edit-distance/"> Edit Distance </a> </td> <td class="s94" dir="ltr" rowspan="2"> ★★★ </td> <td class="s95" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/searching/leetcode-10-regular-expression-matching/"> 10 </a> </td> <td class="s95" dir="ltr"> <a href="https://leetcode.com/problems/wildcard-matching/"> 44 </a> </td> <td class="s95" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-97-interleaving-string/"> 97 </a> </td> <td class="s95" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-115-distinct-subsequences/"> 115 </a> </td> <td class="s91" dir="ltr"> <a href="https://leetcode.com/problems/delete-operation-for-two-strings/"> 583 </a> </td> <td class="s90" dir="ltr" rowspan="2"> I: O(m+n), S = O(mn), T = O(mn) </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R15" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 16 </div> </th> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-712-minimum-ascii-delete-sum-for-two-strings/"> 712 </a> </td> <td class="s95" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-1187-make-array-strictly-increasing/"> 1187 </a> </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-1143-longest-common-subsequence/"> 1143 </a> </td> <td class="s95" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-1092-shortest-common-supersequence/"> 1092 </a> </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-718-maximum-length-of-repeated-subarray/"> 718 </a> </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R16" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 17 </div> </th> <td class="s84" dir="ltr"> 1139 </td> <td class="s88" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-1139-largest-1-bordered-square/"> Largest 1-Bordered Square </a> </td> <td class="s86" dir="ltr"> ★★★ </td> <td class="s84" dir="ltr"> </td> <td class="s84" dir="ltr"> </td> <td class="s84" dir="ltr"> </td> <td class="s84"> </td> <td class="s84"> </td> <td class="s96" dir="ltr"> <div class="softmerge-inner" style="width: 295px; left: -1px;"> I: O(mn), S = O(mn) <br> T = O(mn*min(n,m)) </div> </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R17" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 18 </div> </th> <td class="s84" dir="ltr"> 688 </td> <td class="s88" dir="ltr"> <a href="https://leetcode.com/problems/knight-probability-in-chessboard/"> Knight Probability in Chessboard </a> </td> <td class="s86" dir="ltr"> ★★★ </td> <td class="s91" dir="ltr"> <a href="https://leetcode.com/problems/out-of-boundary-paths/"> 576 </a> </td> <td class="s91" dir="ltr"> <a href="https://leetcode.com/problems/knight-dialer/"> 935 </a> </td> <td class="s84" dir="ltr"> </td> <td class="s84"> </td> <td class="s84"> </td> <td class="s97" dir="ltr"> <div class="softmerge-inner" style="width: 295px; left: -1px;"> I: O(mn) + k <br> S = O(kmn), T = O(kmn) </div> </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R18" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 19 </div> </th> <td class="s92" dir="ltr" rowspan="2"> 322 </td> <td class="s93" dir="ltr" rowspan="2"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-322-coin-change/"> Coin Change </a> </td> <td class="s94" dir="ltr" rowspan="2"> ★★★ </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-377-combination-sum-iv/"> 377 </a> </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-416-partition-equal-subset-sum/"> 416 </a> </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-494-target-sum/"> 494 </a> </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-1043-partition-array-for-maximum-sum/"> 1043 </a> </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/leetcode/leetcode-weekly-contest-137/"> 1049 </a> </td> <td class="s90" dir="ltr" rowspan="2"> I: O(n) + k, S = O(n), T = O(kn) </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R19" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 20 </div> </th> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-1220-count-vowels-permutation/"> 1220 </a> </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-1230-toss-strange-coins/"> 1230 </a> </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-1262-greatest-sum-divisible-by-three/"> 1262 </a> </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-1269-number-of-ways-to-stay-in-the-same-place-after-some-steps/"> 1269 </a> </td> <td class="s84" dir="ltr"> </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R20" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 21 </div> </th> <td class="s84" dir="ltr"> 813 </td> <td class="s88" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-813-largest-sum-of-averages/"> Largest Sum of Averages </a> </td> <td class="s86" dir="ltr"> ★★★★ </td> <td class="s95" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-1278-palindrome-partitioning-iii/"> 1278 </a> </td> <td class="s95" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-1335-minimum-difficulty-of-a-job-schedule/"> 1335 </a> </td> <td class="s95" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-410-split-array-largest-sum/"> 410 </a> </td> <td class="s84"> </td> <td class="s84"> </td> <td class="s97" dir="ltr"> <div class="softmerge-inner" style="width: 295px; left: -1px;"> I: O(n) + k <br> S = O(n*k), T = O(kn^2) </div> </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R21" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 22 </div> </th> <td class="s84" dir="ltr"> 1223 </td> <td class="s88" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-1223-dice-roll-simulation/"> Dice Roll Simulation </a> </td> <td class="s86" dir="ltr"> ★★★★ </td> <td class="s98"> </td> <td class="s84"> </td> <td class="s84"> </td> <td class="s84"> </td> <td class="s84"> </td> <td class="s97" dir="ltr"> <div class="softmerge-inner" style="width: 295px; left: -1px;"> I: O(n) + k + p <br> S = O(k*p), T = O(n^2kp) </div> </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R22" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 23 </div> </th> <td class="s84" dir="ltr"> 312 </td> <td class="s88" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-312-burst-balloons/"> Burst Balloons </a> </td> <td class="s86" dir="ltr"> ★★★★ </td> <td class="s95" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-664-strange-printer/"> 664 </a> </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/leetcode/leetcode-weekly-contest-131-1021-1022-1023-1024/"> 1024 </a> </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/leetcode/leetcode-weekly-contest-135-1037-1038-1039-1040/"> 1039 </a> </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/recursion/leetcode-1140-stone-game-ii/"> 1140 </a> </td> <td class="s91" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/1130-minimum-cost-tree-from-leaf-values/"> 1130 </a> </td> <td class="s97" dir="ltr"> <div class="softmerge-inner" style="width: 295px; left: -1px;"> I: O(n), S = O(n^2), T = O(n^3) </div> </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R23" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 24 </div> </th> <td class="s84" dir="ltr"> 741 </td> <td class="s88" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-741-cherry-pickup/"> Cherry Pickup </a> </td> <td class="s86" dir="ltr"> ★★★★ </td> <td class="s84"> </td> <td class="s84"> </td> <td class="s84"> </td> <td class="s84"> </td> <td class="s84"> </td> <td class="s97" dir="ltr"> <div class="softmerge-inner" style="width: 295px; left: -1px;"> I: O(n^2), S = O(n^3), T = O(n^3) </div> </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R24" style="height: 20px;"> <div class="row-header-wrapper" style="line-height: 20px;"> 25 </div> </th> <td class="s84" dir="ltr"> 546 </td> <td class="s88" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-546-remove-boxes/"> Remove Boxes </a> </td> <td class="s86" dir="ltr"> ★★★★★ </td> <td class="s84"> </td> <td class="s84"> </td> <td class="s84"> </td> <td class="s84"> </td> <td class="s84"> </td> <td class="s97" dir="ltr"> <div class="softmerge-inner" style="width: 295px; left: -1px;"> I: O(n), S = O(n^3), T = O(n^4) </div> </td> </tr> <tr style="height:20px;"> <th class="row-headers-background row-header-shim" id="1674276502R25" style="height: 20px;"> 
<div class="row-header-wrapper" style="line-height: 20px;"> 26 </div> </th> <td class="s84" dir="ltr"> 943 </td> <td class="s88" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/searching/leetcode-943-find-the-shortest-superstring/"> Find the Shortest Superstring </a> </td> <td class="s86" dir="ltr"> ★★★★★ </td> <td class="s95" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/searching/leetcode-980-unique-paths-iii/"> 980 </a> </td> <td class="s95" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/searching/leetcode-996-number-of-squareful-arrays/"> 996 </a> </td> <td class="s95" dir="ltr"> <a href="https://zxi.mytechroad.com/blog/dynamic-programming/leetcode-1125-smallest-sufficient-team/"> 1125 </a> </td> <td class="s84"> </td> <td class="s84"> </td> <td class="s97" dir="ltr"> <div class="softmerge-inner" style="width: 295px; left: -1px;"> I: O(n) <br> S = O(n*2^n), T = (n^2*2^n) 
</div> </td> </tr>
 </tbody> </table> </div> </div> </div>


---
下面结合实例分析
## 70. [爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/)

非常经典！

用$$dp[i]$$表示爬上第i个梯子的方法数。那么
状态转移方程 
$$
dp[i] = dp[i-1] + dp[i-2];
$$

边界条件: $$dp[0] = 1, dp[1]=1$$

## 746. [使用最小花费爬楼梯](https://leetcode-cn.com/problems/min-cost-climbing-stairs/)

用$$dp[i]$$表示爬上第i个梯子的`最小`消耗。那么
状态转移方程 
$$
dp[i] = min{dp[i-1] + cost[i-1], dp[i-2] + cost[i-1]};
$$

边界条件: $$dp[0] = 0, dp[1]=0$$

**总结，这两题能这么做是因为，它们相邻两项的间距是恒定的要么为1，要么为2.**



## 198. [打家劫舍](https://leetcode-cn.com/problems/house-robber/)

> 老dp了，还贪讷

一眼看上去以为是跳跃游戏类似的贪心算法，没想到是老dp换了层皮。

以$dp[i]$表示前ii个元素中最大金额。
我们这样想，第$i-1$个元素$nums[i-1]$是否取到取决于前面一个元素是否取，如果前一个元素不取就是$dp[i-2]+nums[i-1]$，如果前一个元素取到就是$dp[i-1]$。

边值条件$dp[0]=0,dp[1]=nums[0]$，注意下标对应关系。

---
再看跟路径有关的问题

## 64. [最小路径和](https://leetcode-cn.com/problems/minimum-path-sum/)

用$$dp[i][j]$$表示从原点到达(m,n)的`最小`路径和。那么
状态转移方程 
$$
dp[i][j] = min(dp[i][j-1], dp[i-1][j])+grid[i][j];
$$

边界条件: 
$$
dp[0][i] = dp[0][i-1] + grid[0][i](0 \le{i}\le{m}), 
$$
$$
dp[j][0] = dp[j-1][0] + grid[j][0](0 \le{j}\le{n})
$$
这题很特殊的地方是，先求完边界条件才能进行DP操作。

## 62. [不同路径](https://leetcode-cn.com/problems/unique-paths/)

这题和上一题的区别是，不用管路径开销，这样的话我们可以把路径都设为1。

用$$dp[i][j]$$表示从原点到达(m,n)的`不同`路径数目。那么
状态转移方程 
$$
dp[i][j] = dp[i][j-1]+ dp[i-1][j];
$$

边界条件: 
$$
dp[0][i] = 1(0 \le{i}\le{m}), 
$$
$$
dp[j][0] = 1(0 \le{j}\le{n})
$$

## 63. [不同路径2](https://leetcode-cn.com/problems/unique-paths-ii/)

用$$dp[i][j]$$表示从`原点`到$$(i,j)$$的路径总数，只不过这题玩了一点花样，加入障碍物，和`62`异曲同工。上一题我们把边界，包括上边界和左边界，都设为1。这一题，我们想如果遇到障碍物在$$(i,j)$$，那么肯定$$dp[i][j]=0$$对吧？然后对于边界，一旦$$dp[0][j]==0或dp[i][0]==0$$表明，之后的全到不了，因为上左边界分别只有一条路径。


$$ dp[i][j]=\left\{
\begin{array}{lcl}
dp[i-1][j]+dp[i][j-1],       &      & {obstacleGrid[i][j]!=1}\\
0,     &      & {obstacleGrid[i][j]==1}\\
\end{array} \right. $$


>边界
$$
dp[0][j] =\left\{ 
\begin{array}{lcr}
 0, {dp[0][j-1]==0||obstacleGrid[0][j]==0}\\
1, {dp[0][j-1]!=0}\\
\end{array} \right.\\
,
\\
dp[i][0] =\left\{ 
\begin{array}{lcr}
 0, {dp[i-1][0]==0||obstacleGrid[i][0]==0}\\
1, {dp[i-1][0]!=0}\\
\end{array} \right.
$$

**总结，因为路径问题只能向下或向右走和爬楼梯的只能走一步或者两步都是异曲同工的，把状态转移方程和边界条件想出来有助于快速解决问题**

> 此外，涉及到求规律的问题，一般先列出几项再使用dp

## 96. 不同的搜索二叉树

给定一个整数 n，求以 1 ... n 为节点组成的二叉搜索树有多少种？

示例:

```
输入: 3
输出: 5
解释:
给定 n = 3, 一共有 5 种不同结构的二叉搜索树:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

$$
f[i] = \begin{cases}
2×(f[i-1]+···+f[(i-1)/2])+f[i/2]^2,i为奇数\\
2×(f[i-1]+···+f[(i-1)/2])，i为偶数\\
\end{cases}
$$

---

事实上我们在方法一中推导出的 $G(n)$函数的值在数学上被称为卡塔兰数 $C_n $

 。卡塔兰数更便于计算的定义如下:$C_0 = 1, \qquad C_{n+1} = \frac{2(2n+1)}{n+2}C_n$,证明过程可以参考上述文献，此处不再赘述。

> 下面我们看一些富有技巧而实际很简单 的dp问题

## 221. 最大正方形

在一个由 0 和 1 组成的二维矩阵内，找到只包含 1 的最大正方形，并返回其面积。

示例:

```
输入: 

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0

输出: 4
```

扩展85.最大矩形

---



## 53. [最大字序和](https://leetcode-cn.com/problems/maximum-subarray/solution/zui-da-zi-xu-he-by-leetcode-solution/)

给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

```
示例:

输入: [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
```

进阶:

如果你已经实现复杂度为 O(n) 的解法，尝试使用更为精妙的分治法求解。

---

一般人思路是暴力法，我承认，这的确很舒服，但是告诉你有$$O(n)$$的方法，你会怎么想呢。

用$$dp[i]$$，如何表示才具有可行性。刚开始想的是序号从$$0-n-1$$的最大字序和。后来发现存在$$dp[i-1]与nums[i-1]$$断开的情况，而且中间的和一定不大于0. 官解给的是 *以第i个数结尾的连续数组最大和。*也就是不存在断开的情况。妙，实在是妙！
$$
dp[i] = max(dp[i-1]+nums[i-1],num[i-1])
$$
max里面前者表示存在新的后续元素使之更大，后者是新元素比原来的和更大。

>  边界条件：

$$dp[0] = 0$$

此外还可以用滚动数组降低空间复杂度。

## 139.单词拆分

给定一个非空字符串 s 和一个包含非空单词列表的字典 wordDict，判定 s 是否可以被空格拆分为一个或多个在字典中出现的单词。

说明：

拆分时可以重复使用字典中的单词。
你可以假设字典中没有重复的单词。
示例 1：

```
输入: s = "leetcode", wordDict = ["leet", "code"]
输出: true
解释: 返回 true 因为 "leetcode" 可以被拆分成 "leet code"。 
```

---

这一题可以正好填补一些我们思路上的空白。即，动态规划的迭代并不一定是连续的，很有可能存在跳跃。

用$dp[i]$表示s前i个字符能否由字典中单词组成。那么$dp[i]=dp[j]\ \text{and}\  dict.check(s.substr(j,i-j));$，check在这里检查$s[j:i-1]$与字典中某一个单词匹配。初始条件为$dp[0]=true$空字符一定匹配，实际上，dp中大部分元素都是$false$。



## 152. 乘积最大子数组



给你一个整数数组 nums ，请你找出数组中乘积最大的连续子数组（该子数组中至少包含一个数字），并返回该子数组所对应的乘积。

 

示例 1:

```
输入: [2,3,-2,4]
输出: 6
解释: 子数组 [2,3] 有最大乘积 6。

```

示例 2:

```
输入: [-2,0,-1]
输出: 0
解释: 结果不能为 2, 因为 [-2,-1] 不是子数组。
```

---

这道题我们很容易陷入惯性思维，与最大子序和相似，我们可以设定$dp[i]$为以$nums[i-1]$为末尾的最大乘积，很容易知道 
$$
dp[i]=max\{dp[i-1]*nums[i-1],nums[i-1]\}
$$
但是这一题与53不同的是，负负得正，比如$[-9,1,-8]$得到最大和是72而不是1. 所以我们需要分类讨论，$num[i-1]$正负性，还要设计一个求最小积的$mdp[i]$，与求最大积$Mdp[i]$相对，具体如下：
$$
Mdp=\begin{cases}
	\max\{Mdp[i-1]*nums[i-1],nums[i-1]\},nums[i-1]>0\\
	\max\{mdp[i-1]*nums[i-1],nums[i-1]\},otherwise\\
	\end{cases}\\
	\\\
	\\\ 
	\\\
mdp=\begin{cases}
	\min\{mdp[i-1]*nums[i-1],nums[i-1]\},nums[i-1]>0\\
	\min\{Mdp[i-1]*nums[i-1],nums[i-1]\},otherwise\\
	\end{cases}
$$
初始条件$mdp[1]=nums[0],Mdp[1]=nums[0].$

---
>下面我们看一些复杂的DP问题。

## 410. [分割数组的最大和](https://leetcode-cn.com/problems/split-array-largest-sum/)

给定一个非负整数数组和一个整数 m，你需要将这个数组分成 m 个非空的连续子数组。设计一个算法使得这 m 个子数组各自和的最大值最小。

注意:
数组长度 n 满足以下条件:

* 1 ≤ n ≤ 1000
* 1 ≤ m ≤ min(50, n)

示例:
```
输入:
nums = [7,2,5,10,8]
m = 2

输出:
18

解释:
一共有四种方法将nums分割为2个子数组。
其中最好的方式是将其分为[7,2,5] 和 [10,8]，
因为此时这两个子数组各自的和的最大值为18，在所有情况中最小。
```

---

`将数组分割为m段，求...`是动态规划的常见问法。

我们可以令$$dp[i][j]$$表示数组前$$i$$个数分割为$$j$$段，所能得到最大连续子数组和的最小值，我们可以考虑第$$j$$段的具体范围，即我们可以枚举$$k$$，将前$$k$$个数分割为$$j-1$$段，而第$$k+1$$到第$$i$$个数为第$$j$$段，此时，这$$j$$段数组中和的最大值等于$$dp[k][j-1]$$与$$sum(k+1,i)$$中和的较大值，其中$$sum(a,b)$$表示$$nums[i]在[a,b]$$的范围和。

状态转移方程：

$$
dp[i][j]=\min\limits_{k=0}^{i-1}(\max(dp[k][j-1],\sum\limits_{k+1}^i{nums[i]})
$$

边界条件:
$$
dp[0][0] = 0;
$$

时间复杂度: $$O(n^2m)$$,其中$$n$$是数组长度，$$m$$是分成非空的连续子数组个数，总状态数$$O(n×m)$$,状态转移时间$$O(n)$$。
空间复杂度：$$O(n×m)$$为动态规划数组开销。



> "我🤮饱了，后面还有吗" 
>
> “当然”

下面介绍一下字符串中的dp解法，比如10. 正则表达式匹配 和 44. 通配符匹配。 都是很经典的dp。 寥寥几句足以把超复杂的可能性涵盖其中，真让人不尽感叹造物主的鬼斧神工。



# 10.[正则表达式匹配](https://leetcode-cn.com/problems/regular-expression-matching/)

给你一个字符串 s 和一个字符规律 p，请你来实现一个支持 '.' 和 '*' 的正则表达式匹配。

```
'.' 匹配任意单个字符
'*' 匹配零个或多个前面的那一个元素
```

所谓匹配，是要涵盖 整个字符串 s的，而不是部分字符串。

说明:

s 可能为空，且只包含从 a-z 的小写字母。
p 可能为空，且只包含从 a-z 的小写字母，以及字符 . 和 *。
示例 1:

```
输入:
s = "aa"
p = "a"
输出: false
解释: "a" 无法匹配 "aa" 整个字符串。
```

示例 2:

```
输入:
s = "aa"
p = "a*"
输出: true
解释: 因为 '*' 代表可以匹配零个或多个前面的那一个元素, 在这里前面的元素就是 'a'。因此，字符串 "aa" 可被视为 'a' 重复了一次。
```

示例 3:

```
输入:
s = "ab"
p = ".*"
输出: true
解释: ".*" 表示可匹配零个或多个（'*'）任意字符（'.'）。
```

示例 4:

```
输入:
s = "aab"
p = "c*a*b"
输出: true
解释: 因为 '*' 表示零个或多个，这里 'c' 为 0 个, 'a' 被重复一次。因此可以匹配字符串 "aab"。
```
示例5
```
输入:
s = "mississippi"
p = "mis*is*p*."
输出: false
```
---

我们用 $$dp[i][j]$$ 表示 s 的前 i 个字符与 pp 中的前 j 个字符是否能够匹配。在进行状态转移时，我们考虑 pp 的第 jj 个字符的匹配情况：

* 如果 p 的第 j 个字符是一个小写字母，那么我们必须在 s 中匹配一个相同的小写字母，即
  $$
  dp[i][j] =  (s[i-1]==p[j-1] \&\& dp[i-1][j-1]
  $$


如果我们通过这种方法进行转移，那么我们就需要枚举这个组合到底匹配了 ss 中的几个字符，会增导致时间复杂度增加，并且代码编写起来十分麻烦。我们不妨换个角度考虑这个问题：字母 + 星号的组合在匹配的过程中，本质上只会有两种情况：

* 匹配 s 末尾的一个字符，将该字符扔掉，而该组合还可以继续进行匹配；

* 不匹配字符，将该组合扔掉，不再进行匹配。

如果按照这个角度进行思考，我们可以写出很精巧的状态转移方程：

$$
dp[i][j]=\left\{
\begin{array}{lcr}
dp[i-1][j]||dp[i][j-2],\ s[i]==p[j-1]
\\
dp[i][j-2],\ s[i]\ne p[j-1]
\end{array}
\right.
$$

* 在任意情况下，只要 $$p[j]$$ 是` .`，那么 $$p[j]$$ 一定成功匹配 ss 中的任意一个小写字母。

最终的状态转移方程如下：

$$
dp[i][j] = 
\begin{cases}
\text{if}\ (p[j]\ne '*')=\begin{cases}
dp[i-1][j-1], matches(s[i],p[j]) \\
false, \ otherwise
\end{cases}
\\
\\
otherwise = \begin{cases}
dp[i-1][j]\ || \ dp[i][j-2], \ matches(s[i],p[j-1])
\\
dp[i][j-2], otherwise
\end{cases}
\end{cases}
$$

其中$$ \textit{matches}(x, y)$$ 判断两个字符是否匹配的辅助函数。只有当 y 是 `.` 或者 x 和 y 本身相同时，这两个字符才会匹配。

>  细节

动态规划的边界条件为 $$ dp[0][0] = true $$，即两个空字符串是可以匹配的。最终的答案即为 $$dp[m][n]$$，其中 m和 n 分别是字符串 s 和 p 的长度。由于大部分语言中，字符串的字符下标是从 0 开始的，因此在实现上面的状态转移方程时，需要注意状态中每一维下标与实际字符下标的对应关系。

在上面的状态转移方程中，如果字符串 p 中包含一个字符+星号的组合（例如 $$a*$$），那么在进行状态转移时，会先将 a 进行匹配（当 $$p[j]$$ 为 a 时），再将 a* 作为整体进行匹配（当 $$p[j]$$ 为 * 时）。然而，在题目描述中，我们必须将 a* 看成一个整体，因此将 a 进行匹配是不符合题目要求的。看来我们进行了额外的状态转移，这样会对最终的答案产生影响吗？这个问题留给读者进行思考。

C++代码

```C++
class Solution {
public:
    bool isMatch(string s, string p) {
        int m = s.size();
        int n = p.size();

        auto matches = [&](int i, int j) {
            if (i == 0) {
                return false;
            }
            if (p[j - 1] == '.') {
                return true;
            }
            return s[i - 1] == p[j - 1];
        };

        vector<vector<int>> f(m + 1, vector<int>(n + 1));
        f[0][0] = true;
        for (int i = 0; i <= m; ++i) {
            for (int j = 1; j <= n; ++j) {
                if (p[j - 1] == '*') {
                    f[i][j] |= f[i][j - 2];
                    if (matches(i, j - 1)) {
                        f[i][j] |= f[i - 1][j];
                    }
                }
                else {
                    if (matches(i, j)) {
                        f[i][j] |= f[i - 1][j - 1];
                    }
                }
            }
        }
        return f[m][n];
    }
};

```





# 44. [通配符匹配](https://leetcode-cn.com/problems/wildcard-matching/)

给定一个字符串 (s) 和一个字符模式 (p) ，实现一个支持 '?' 和 '*' 的通配符匹配。

```C++
'?' 可以匹配任何单个字符。
'*' 可以匹配任意字符串（包括空字符串）。
两个字符串完全匹配才算匹配成功。
```

说明:

* s 可能为空，且只包含从 a-z 的小写字母。
* p 可能为空，且只包含从 a-z 的小写字母，以及字符 ? 和 *。

---

我们用$$dp[i][j]$$表示s的第$$i$$个字符与p的第$$j$$个字符是否匹配。

* 第一种情况是字母与字母匹配，即
  $$
  dp[i][j] =  (s[i-1]==p[j-1] \&\& dp[i-1][j-1])
  $$

* 第二种情况是$$p[j]$$是问好，则对$$s[i]$$没有任何要求
  $$
  dp[i][j] = (p[j-1]=='?'\&\&dp[i-1][j-1])
  $$

* 第三种情况，是遇到$$''*''$$，这种情况最为复杂，因为不知道星号要匹配多少个字符，这里很容易想到`回溯`方法，但是回溯一般会超时，著名的KMP算法是因为了避免回溯才会那么快。

  所以我们想这个星号可以使用多次，也可以一次都不使用。
  $$
  dp[i][j] = dp[i-1][j]||dp[i][j-1]
  $$
  后面一项表示不使用星号，前面一项表示使用星号。

  总结一下：
  $$
  dp[i][j]=\left\{
  \begin{array}{lcr}
  s[i-1]==p[j-1] \&\& dp[i-1][j-1]，'a-z'
  \\
  p[j-1]=='?'\&\&dp[i-1][j-1],'?'
  \\
  dp[i-1][j]||dp[i][j-1], '*'
  \end{array}
  \right.
  $$
  

  > 边界条件：

  也就是$$dp[0][0]$$，我们不能单纯认为开始两个字符相等就是$$dp[0][0]==True$$。因为$$p$$有星号和问号开头的情况。
  $$
  dp[0][0]=(s[0]==p[0])||(p[0]=='?')||(p[0]=='*')
  $$

  1. 若两个字符串为空，$$dp[0][0]$$也为True.

  
  $$
  dp[i][0]=!s.size()
  $$
  即空字符串无法匹配非空字符串。

  2. 若s为空，p全为"*"，才能完成匹配。
     $$
     dp[0][j] = (p[j]=='*')\&\&dp[0][j-1]
     $$

  

我们可以发现，$$dp[i][0]$$的值恒为假，$$dp[0][j]$$ 在 $$j$$ 大于模式 $$p$$ 的开头出现的星号字符个数之后，值也恒为假，而 $$dp[i][j]$$ 的默认值（其它情况）也为假，因此在对动态规划的数组初始化时，我们就可以将所有的状态初始化为 False，减少状态转移的代码编写难度。

此外还要考虑字符串的硬边界。此外，**注意**下标对$$dp[i][j]$$表示$$s[i-1]$$与$$p[j-1]$$匹配，因为下标是从0开始的。

Python 实现：

```python
      def isMatch(self, s: str, p: str) -> bool:
          if not p and s: return False
          if not s and not p: return True 
              
          m = len(s); n = len(p)
          dp = [[False for _ in range(n+1)] for _ in range(m+1) ]
          dp[0][0] = (p[0]=='?') or (p[0]=='*') or (s and s[0]==p[0]) 
          for i in range(1,m+1):
              dp[i][0] = not len(s)
          for j in range(1,n+1):
              dp[0][j] = (p[j-1] == '*') and dp[0][j-1]
          for i in range(1,m+1):
              for j in range(1,n+1):
                  dp[i][j] = (s[i-1] == p[j-1] and dp[i-1][j-1]) or \
                              (p[j-1] == '?' and dp[i-1][j-1]) or \
                              (p[j-1] == '*' and (dp[i-1][j] or dp[i][j-1]))
                  print("(%d,%d):"%(i,j),dp[i][j])
          return dp[m][n]
```



C++实现：

```C++
class Solution {
public:
bool isMatch(string s, string p)
    {
        if (!p.size() && s.size()) return false;
        if (!s.size() && !p.size()) return true;
        int m = s.size(), n = p.size();
        vector<vector<bool>> dp(m+1,vector<bool>(n+1,false));
        dp[0][0] = (p[0]=='?')||(p[0]=='*')||(s.size()&&s[0]==p[0]);
        for(int i = 1; i < m+1; i++) dp[i][0] = !s.size();
        for(int j = 1; j < n+1; j++) dp[0][j] = (p[j-1]=='*') && dp[0][j-1];
        for(int i = 1; i < m+1; i++)
        for(int j = 1; j < n+1; j++)
        dp[i][j] = (s[i-1] == p[j-1] && dp[i-1][j-1]) || \
                            (p[j-1] == '?' && dp[i-1][j-1]) || \
                            (p[j-1] == '*' && (dp[i-1][j] || dp[i][j-1]));
        return dp[m][n];            
    }
};
```

![image-20200727202600791](.\img\image-20200727202600791.png)

明显是C++要快些()，嘻嘻😂，而且内存占用要小些

老规矩，下面分析时间复杂度和空间复杂度.

时间复杂度：$$O(MN)$$

空间复杂度:$$O(NM)$$ $$N和M$$分别表示目标串和模式串的长度。我们可以使用`滚动数组`对空间进行优化，即用两个长度为 $$n+1$$ 的一维数组代替整个二维数组进行状态转移，空间复杂度为$$ O(n)$$。

当然这题也有贪心解法，我们专门放在[[深入剖析贪心算法]()]去讲。



# 72 [编辑距离](https://leetcode-cn.com/problems/edit-distance/)

这一题在LC上属于难题分类，但实际上通过率高达59.6%，是一道名副其实的`Easy`题。

但是我们想说的dp千变万化，不离其宗。题目做多了自然就有想法了。

给你两个单词 word1 和 word2，请你计算出将 word1 转换成 word2 所使用的最少操作数 。

你可以对一个单词进行如下三种操作：

1. 插入一个字符
2. 删除一个字符
3. 替换一个字符

---

我们用$$dp[i][j]$$表示word1前i个字符转换为word2前j个字符所需的`最小`操作数。 

然后在word1插入一个字符相当于$$dp[i][j]=dp[i-1][j]+1$$，一定会多出来一个步骤。

然后在word1删除一个字符相当于$$dp[i][j]=dp[i][j-1]+1$$，也一定会多出来一个步骤。

如果word1最后一个字符通过替换得到word2，那么要分情况，如果最后一个字符相同，那么$$dp[i][j]=dp[i-1][j-1]$$，否则$$dp[i][j]=dp[i-1][j-1]+1$$.

> 边界条件

$$dp[0][j] = j,dp[i][0]=i$$

就是完全的删除或者完全插入。

代码C++

```C++
class Solution {
public:
    int minDistance(string word1, string word2) {
        if(!word1.size()) return word2.size();
        if(!word2.size()) return word1.size();
        //dp[i][j]表示word1的前i位替换为word2前i位所需的最小步数
        int m = word1.size(), n = word2.size();
        vector<vector<int>> dp(m+1,vector<int>(n+1));
        dp[0][0] = 0;
        dp[1][1] = (word1[0]==word2[0])? 0:1;
        for(int i = 1; i <=m ;i++) dp[i][0] = i;
        for(int j = 1; j <=n ;j++) dp[0][j] = j;
        for(int i = 1; i <=m; i++ )
        for(int j = 1; j <=n; j++ )
        {
            int exchange = (word1[i-1]==word2[j-1])?dp[i-1][j-1]:dp[i-1][j-1]+1;
            dp[i][j] = min(exchange, min(dp[i-1][j]+1,dp[i][j-1]+1));
        }
        return dp[m][n];
    }
};
```

