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

题目中的匹配是一个「逐步匹配」的过程：我们每次从字符串 pp 中取出一个字符或者「字符 + 星号」的组合，并在 ss 中进行匹配。对于 pp 中一个字符而言，它只能在 ss 中匹配一个字符，匹配的方法具有唯一性；而对于 pp 中字符 + 星号的组合而言，它可以在 ss 中匹配任意自然数个字符，并不具有唯一性。因此我们可以考虑使用动态规划，对匹配的方案进行枚举。

我们用 f[i][j]f[i][j] 表示 ss 的前 ii 个字符与 pp 中的前 jj 个字符是否能够匹配。在进行状态转移时，我们考虑 pp 的第 jj 个字符的匹配情况：

如果 pp 的第 jj 个字符是一个小写字母，那么我们必须在 ss 中匹配一个相同的小写字母，即

f[i][j] = \begin{cases} f[i - 1][j - 1], & s[i] = p[j]\\ \text{false}, & s[i] \neq p[j] \end{cases}
f[i][j]={ 
f[i−1][j−1],
false,
	

s[i]=p[j]
s[i] 

	
 =p[j]
	


也就是说，如果 ss 的第 ii 个字符与 pp 的第 jj 个字符不相同，那么无法进行匹配；否则我们可以匹配两个字符串的最后一个字符，完整的匹配结果取决于两个字符串前面的部分。

如果 pp 的第 jj 个字符是 *，那么就表示我们可以对 pp 的第 j-1j−1 个字符匹配任意自然数次。在匹配 00 次的情况下，我们有

f[i][j] = f[i][j - 2]
f[i][j]=f[i][j−2]

也就是我们「浪费」了一个字符 + 星号的组合，没有匹配任何 ss 中的字符。

在匹配 1,2,3, \cdots1,2,3,⋯ 次的情况下，类似地我们有

\begin{aligned} & f[i][j] = f[i - 1][j - 2], \quad && \text{if~} s[i] = p[j - 1] \\ & f[i][j] = f[i - 2][j - 2], \quad && \text{if~} s[i - 1] = s[i] = p[j - 1] \\ & f[i][j] = f[i - 3][j - 2], \quad && \text{if~} s[i - 2] = s[i - 1] = s[i] = p[j - 1] \\ & \cdots\cdots & \end{aligned}
	

f[i][j]=f[i−1][j−2],
f[i][j]=f[i−2][j−2],
f[i][j]=f[i−3][j−2],
⋯⋯
	

​	

if s[i]=p[j−1]
if s[i−1]=s[i]=p[j−1]
if s[i−2]=s[i−1]=s[i]=p[j−1]
	


如果我们通过这种方法进行转移，那么我们就需要枚举这个组合到底匹配了 ss 中的几个字符，会增导致时间复杂度增加，并且代码编写起来十分麻烦。我们不妨换个角度考虑这个问题：字母 + 星号的组合在匹配的过程中，本质上只会有两种情况：

匹配 ss 末尾的一个字符，将该字符扔掉，而该组合还可以继续进行匹配；

不匹配字符，将该组合扔掉，不再进行匹配。

如果按照这个角度进行思考，我们可以写出很精巧的状态转移方程：

f[i][j] = \begin{cases} f[i - 1][j] \text{~or~} f[i][j - 2], & s[i] = p[j - 1] \\ f[i][j - 2], & s[i] \neq p[j - 1] \end{cases}
f[i][j]={ 
f[i−1][j] or f[i][j−2],
f[i][j−2],
	

s[i]=p[j−1]
s[i] 

	
 =p[j−1]
	


在任意情况下，只要 p[j]p[j] 是 .，那么 p[j]p[j] 一定成功匹配 ss 中的任意一个小写字母。

最终的状态转移方程如下：

f[i][j] = \begin{cases} \text{if~} (p[j] \neq \text{~`*'}) = \begin{cases} f[i - 1][j - 1], & \textit{matches}(s[i], p[j])\\ \text{false}, & \text{otherwise} \end{cases} \\ \text{otherwise} = \begin{cases} f[i - 1][j] \text{~or~} f[i][j - 2], & \textit{matches}(s[i], p[j-1]) \\ f[i][j - 2], & \text{otherwise} \end{cases} \end{cases}
f[i][j]= 
⎩
⎪
⎪
⎪
⎪
⎪
⎨
⎪
⎪
⎪
⎪
⎪
⎧
	

if (p[j] 

	
 = ‘*’)={ 
f[i−1][j−1],
false,
	

matches(s[i],p[j])
otherwise
	

otherwise={ 
f[i−1][j] or f[i][j−2],
f[i][j−2],
	

matches(s[i],p[j−1])
otherwise
	

​	


其中 \textit{matches}(x, y)matches(x,y) 判断两个字符是否匹配的辅助函数。只有当 yy 是 . 或者 xx 和 yy 本身相同时，这两个字符才会匹配。

细节

动态规划的边界条件为 f[0][0] = \text{true}f[0][0]=true，即两个空字符串是可以匹配的。最终的答案即为 f[m][n]f[m][n]，其中 mm 和 nn 分别是字符串 ss 和 pp 的长度。由于大部分语言中，字符串的字符下标是从 00 开始的，因此在实现上面的状态转移方程时，需要注意状态中每一维下标与实际字符下标的对应关系。

在上面的状态转移方程中，如果字符串 pp 中包含一个字符+星号的组合（例如 a*），那么在进行状态转移时，会先将 a 进行匹配（当 p[j]p[j] 为 a 时），再将 a* 作为整体进行匹配（当 p[j]p[j] 为 * 时）。然而，在题目描述中，我们必须将 a* 看成一个整体，因此将 a 进行匹配是不符合题目要求的。看来我们进行了额外的状态转移，这样会对最终的答案产生影响吗？这个问题留给读者进行思考。





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