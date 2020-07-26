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