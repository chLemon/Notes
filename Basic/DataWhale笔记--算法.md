# 【Datawhale组队学习2020.8】LeetCode（//TODO）

# Task01 分治

## 主要思想

分治算法的主要思想是将原问题递归地分成若干个子问题，直到子问题满足边界条件，停止递归。将子
问题逐个击破(一般是同种方法)，将已经解决的子问题合并，最后，算法会层层合并得到原问题的答
案。

## 分治算法的步骤

分：递归地将问题分解为各个的子问题(性质相同的、相互独立的子问题)；
治：将这些规模更小的子问题逐个击破；
合：将已解决的子问题逐层合并，最终得出原问题的解；

## 分治法适用的情况

原问题的计算复杂度随着问题的规模的增加而增加。
原问题能够被分解成更小的子问题。
子问题的结构和性质与原问题一样，并且相互独立，子问题之间不包含公共的子子问题。
原问题分解出的子问题的解可以合并为该问题的解。

## 一些想法

将大问题分解为小问题，或者说转换为一些小步骤是一种很常用的思路。减而治之、分而治之、贪心算法、动态规划的主要思路都是这样。我认为分治法最大的特点在于，将大问题分解时，一般是分为规模相当的两个子问题，这样可以有效的将复杂度控制在对数级别上。

分治法真正的难点应该在于如何将小问题的答案合并成大问题的答案。如何合，决定了如何分。

## 算法题

### Leetcode 169. 多数元素

#### 题目描述

给定一个大小为n 的数组，找到其中的众数。众数是指在数组中出现次数大于[n/2] 的元素。
你可以假设数组是非空的，并且给定的数组总是存在众数。

示例1:

```
输入: [3,2,3]
输出: 3
```

示例2:

```
输入: [2,2,1,1,1,2,2]
输出: 2
```

#### 思路1：分治

复杂度$$O(nlogn)$$

教程上的思路：

+ 确定切分的终止条件：
  直到所有的子问题都是长度为1 的数组，停止切分。

+ 准备数据，将大问题切分为小问题：
  递归地将原数组二分为左区间与右区间，直到最终的数组只剩下一个元素，将其返回

+ 处理子问题得到子结果，并合并：
  长度为1 的子数组中唯一的数显然是众数，直接返回即可。
  如果它们的众数相同，那么显然这一段区间的众数是它们相同的值。
  如果他们的众数不同，比较两个众数在整个区间内出现的次数来决定该区间的众数

##### 代码

```java
public int majorityElement(int[] nums) {
    return majorityElement(nums, 0, nums.length - 1);
}

public int majorityElement(int[] nums, int lo, int hi) {
    if (hi == lo) {
        return nums[lo];
    }
    int mid = (hi - lo) / 2 + lo;
    int left = majorityElement(nums, lo, mid);
    int right = majorityElement(nums, mid + 1, hi);

    if (left == right) {
        return left;
    } else {
        return count(nums, lo, mid, left) > count(nums, mid + 1, hi, right) ? left : right;
    }
}

public int count(int[] nums, int lo, int hi, int k) {
    int count = 0;
    for (int i = lo; i <= hi; i++) {
        if (nums[i] == k) {
            count++;
        }
    }
    return count;
}
```

#### 思路2：减而治之

这题 算法与数据结构 课上讲过。用减而治之，复杂度$$O(n)$$

主要利用这样一个性质：将长度为n的数组分为两个子数组，记为p、q，记数组n的众数为k，若p中的k的次数小于等于p长度的一半，那么q的众数也是k。

证明略。我们要利用的就是p中k恰好为p一半时，q的众数依旧是k这一点。

从数组左侧开始，记第一个元素为a，指针右移，当a的出现次数为指针左侧数组的一半时，去掉这部分。直到最后只剩下一个元素，该元素就是答案。如果一个都不剩，那么最后一个数组的第一个元素就是答案。

##### 代码

```java
public int majorityElement(int[] nums) {
    int lo = 0;
    int hi = 1;
    int count = 1;
    while (hi < nums.length) {
        if (nums[hi] == nums[lo]) {
            count++;
        }
        if (hi - lo + 1 == 2 * count) {
            lo = ++hi;
            count = 1;
        }
        hi++;
    }
    return nums[lo];
}
```

### Leetcode 53. 最大子序和

#### 题目描述

给定一个整数数组nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返
回其最大和。

示例：

```
输入: [-2,1,-3,4,-1,2,1,-5,4],
输出: 6
解释: 连续子数组[4,-1,2,1] 的和最大为6。
```

#### 思路1：分治

略。说真的，看了眼教程上的算法大概思路，头有点大，一点也不想实现。

#### 思路2：动态规划

这道题要求一个**连续的子数组**的某种东西最大，这种通常都可以用DP做。

从左往右，计算以nums[i]结尾的子数组的最大和。

计算方法：当以nums[i-1]结尾的子数组的最大和为正数的时候，那么就加上。如果是负数，那么就不管。

最后遍历一遍拿到最大值即可。

复杂度：$$O(n)$$

##### 代码

```java
public int maxSubArray(int[] nums) {
    for (int i = 1; i < nums.length; i++) {
        nums[i] += nums[i - 1] > 0 ? nums[i - 1] : 0;
    }
    int result = nums[0];
    for (int i = 1; i < nums.length; i++) {
        result = nums[i] > result ? nums[i] : result;
    }
    return result;
}
```

### Leetcode 50. Pow(x, n)

#### 题目描述

实现pow(x, n) ，即计算x 的n 次幂函数。

示例1:

```
输入: 2.00000, 10
输出: 1024.00000
```

示例2:

```
输入: 2.10000, 3
输出: 9.26100
```

示例3:

```
输入: 2.00000, -2
输出: 0.25000
解释: 2-2 = 1/22 = 1/4 = 0.25
```

说明:
-100.0 < x < 100.0
n 是32 位有符号整数，其数值范围是$$[-2^{31},2^{31}-1]$$。

#### 思路

这道题目是非常典型的分治（符合我对分治的理解）。每次把问题划分为规模相当的2部分，然后合并也很方便。

这道题的重点就是如何降低时间复杂度，暴力算法一个一个乘的复杂度为$$O(n)$$，通过$$a^n=a^{\frac12 *2}$$可以直接把复杂度降至$$O(logn)$$。

教程上的思路：

+ 确定切分的终止条件
  对n 不断除以2，并更新n ，直到为0，终止切分
+ 准备数据，将大问题切分为小问题
  对n 不断除以2，更新
+ 处理子问题得到子结果，并合并
  x 与自身相乘更新x
  如果n%2 ==1
  将p 乘以x 之后赋值给p (初始值为1)，返回p
  最终返回p

#### 代码

```java
public double myPow(double x, int n) {
    if (n == 0 || x == 0) {
        return 1;
    }
    if (n == 1) {
        return x;
    }
    if (n == 2) {
        return x * x;
    }
    if (n < 0) {
        return 1 / x / myPow(x, -n - 1);
    }
    double temp = myPow(x, n / 2);
    return (n & 1) == 0 ? temp * temp : temp * temp * x;
}
```

# Task 02 动态规划

动态规划常常适用于有重叠子问题和最优子结构性质的问题，

## 主要思想

+ 若要解一个给定问题，我们需要解其不同部分（即子问题），再根据子问题的解以得出原问题的解。动
  态规划往往用于优化递归问题，例如斐波那契数列，如果运用递归的方式来求解会重复计算很多相同的
  子问题，利用动态规划的思想可以减少计算量。
+ 动态规划法仅仅解决每个子问题一次，具有天然剪枝的功能，从而减少计算量，
+ 一旦某个给定子问题的解已经算出，则将其记忆化存储，以便下次需要同一个子问题解之时直接查表。

## 动态规划模板步骤：

1. 确定动态规划状态
2. 写出状态转移方程（画出状态转移表）
3. 考虑初始化条件
4. 考虑输出状态
5. 考虑对时间，空间复杂度的优化（Bonus）

## 一些想法

动态规划的算法题非常多，在《剑指Offer》中曾提到适用于动态规划问题的三个特点：

1. 问题是最优化问题
2. 整体问题依赖于子问题的最优解。也就是说子问题也是最优化问题，并且整体问题的解可以通过子问题的解推导。
3. 子问题间有重叠的更小问题

在实际做题的过程中，DP给我感觉是，整体问题可以看做是一个序列问题中的一步，是一个问题规模不断上升的过程。有点像**数学归纳法**。而解决DP问题的关键就在于如何去划分“状态”，状态之间又是如何转移的。

## 算法题

### Leetcode 300.最长上升子序列

#### 题目描述

给定一个无序的整数数组，找到其中最长上升子序列的长度。

```
示例:
输入: [10,9,2,5,3,7,101,18]
输出: 4
解释: 最长的上升子序列是[2,3,7,101]，它的长度是4。
```

#### 思路1：DP

状态：dp[i]表示以i结尾的最长上升子序列的长度

状态转移：如果数组的第i+1个值，恰好比第i个值大，那么$$dp[i+1]=dp[i]+1$$。以此类推，遍历0~i的值，如果第i+1比第0大，那么dp[i+1]可能的取值就有dp[0]+1【最长串恰好是i+1跟在了dp[0]对应的那个串后面】；如果第i+1比第1大，那么dp[i+1]的可能取值就有dp[1]+1……dp[i+1]的取值为这些可能值中的最大值。

#### 代码

```java
    public int lengthOfLIS(int[] nums) {
        if(nums.length == 0) return 0;
        int[] dp = new int[nums.length];
        for (int i = 0; i < dp.length; i++) {
            dp[i]=1;
        }
        for (int i = 1; i < nums.length; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) {
                    dp[i] = Math.max(dp[i], dp[j]+1);
                } 
            }
        }
        int result = dp[0];
        for (int i = 0; i < dp.length; i++) {
            result = result< dp[i]?dp[i]:result;
        }
        return result;
    }
```

#### 思路2：DP+二分

此处可以对状态转移过程进行优化，将复杂度降低到O(logn)。该思路请参考LeetCode题解。

#### 代码

```java
    public int lengthOfLIS(int[] nums) {
        int[] tails = new int[nums.length];
        int res = 0;
        for(int num : nums) {
            int i = 0, j = res;
            while(i < j) {
                int m = (i + j) / 2;
                if(tails[m] < num) i = m + 1;
                else j = m;
            }
            tails[i] = num;
            if(res == j) res++;
        }
        return res;
    }
```

### Leetcode 674.最长连续递增序列

#### 题目描述

给定一个未经排序的整数数组，找到最长且连续的的递增序列。

```
示例1:
输入: [1,3,5,4,7]
输出: 3
解释: 最长连续递增序列是[1,3,5], 长度为3。
尽管[1,3,5,7] 也是升序的子序列, 但它不是连续的，因为5和7在原数组里被4隔开。
```

#### 思路

和上一题相比，这题要求连续，简单了许多。

#### 代码


```java
public int findLengthOfLCIS(int[] nums) {
    int result = 0;
    if (nums == null || nums.length == 0) {
        return result;
    }
    int temp = 1;
    result = 1;
    for (int i = 1; i < nums.length; i++) {
        if (nums[i] > nums[i - 1]) {
            result = ++temp > result ? temp : result;
        } else {
            temp = 1;
        }
    }
    return result;
}
```

### Leetcode5. 最长回文子串

#### 题目描述

给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。

```
示例 1：
输入: "babad"
输出: "bab"
注意: "aba" 也是一个有效答案。
```

#### 思路

状态：```dp[i][j]```表示子串s从```i```到```j```是否为回文子串。

状态转移方程：

```
if s[i]==s[j]:
    if j-i<3:
    dp[i][j]=True
else:
    dp[i][j]=dp[i+1][j-1]
```

**这个是一个二维dp的经典题目，需要注意的就是定义dp数组的状态是什么，这里不用长度作为dp值而用是否是回文子串这个状态来存储也是一个比较巧妙的方法，使得题目变得容易理解。**

#### 代码

```java
public String longestPalindrome(String s) {
    // 特判
    int len = s.length();
    if (len < 2) {
        return s;
    }

    int maxLen = 1;
    int begin = 0;

    // dp[i][j] 表示 s[i, j] 是否是回文串
    boolean[][] dp = new boolean[len][len];
    char[] charArray = s.toCharArray();

    for (int i = 0; i < len; i++) {
        dp[i][i] = true;
    }
    for (int j = 1; j < len; j++) {
        for (int i = 0; i < j; i++) {
            if (charArray[i] != charArray[j]) {
                dp[i][j] = false;
            } else {
                if (j - i < 3) {
                    dp[i][j] = true;
                } else {
                    dp[i][j] = dp[i + 1][j - 1];
                }
            }

            // 只要 dp[i][j] == true 成立，就表示子串 s[i..j] 是回文，此时记录回文长度和起始位置
            if (dp[i][j] && j - i + 1 > maxLen) {
                maxLen = j - i + 1;
                begin = i;
            }
        }
    }
    return s.substring(begin, begin + maxLen);
}
```

```java
    public String longestPalindrome(String s) {
        if (s.length() == 0) {
            return "";
        }
        if (s.length() < 2) {
            return s;
        }

        boolean[][] dp = new boolean[s.length()][s.length()];
        dp[0][0] = true;

        int maxLen = 0; // 这里初始值设置成1的话，后面就可以在循环体里面直接判断了
        int start = 0;

        for (int i = 1; i < s.length(); i++) {
            dp[i][i] = true;
            dp[i][i-1] = true;
        }
        for (int j = 1; j < s.length(); j++) {
            for (int i = 0; i < j; i++) {
                dp[i][j] = dp[i + 1][j - 1] && (s.charAt(i) == s.charAt(j));
            }
        }
        for (int i = 0; i < s.length(); i++) {
            for (int j = i; j < s.length(); j++) {
                if (dp[i][j] && j - i + 1 > maxLen) {
                    maxLen = j - i + 1;
                    start = i;
                }
            }
        }
        return s.substring(start, start + maxLen);
    }
```

### Leetcode516. 最长回文子序列

#### 题目描述

给定一个字符串s，找到其中最长的回文子序列。可以假设s的最大长度为1000。

```
示例 1:
输入:
"bbbab"
输出:
4
```

#### 思路

状态：```二维的 dp[i][j] 来表示字符串第 i 个字符到第 j 个字符的长度```

状态转移方程：

```
if s[i]==s[j]:
    dp[i][j]= dp[i+1][j-1]+2
else:
    dp[i][j]=max(dp[i][j-1],dp[i+1][j])
```

#### 代码

```
    public int longestPalindromeSubseq(String s) {

        int[][] dp = new int[s.length()][s.length()];

        //初始化
        for (int i = 0; i < s.length(); i++) {
            dp[i][i] = 1;
        }
        int result = 1;
        for (int i = s.length() - 1; i >= 0; i--) {
            for (int j = i + 1; j < s.length(); j++) {
                if (s.charAt(i) == s.charAt(j)) {
                    dp[i][j] = dp[i + 1][j - 1] + 2;
                } else {
                    dp[i][j] = Math.max(dp[i + 1][j], dp[i][j - 1]);
                }
                if (dp[i][j] > result) {
                    result = dp[i][j];
                }
            }
        }
        return result;
    }
```

### Leetcode72. 编辑距离

#### 题目描述

给定两个单词 word1 和 word2，计算出将 word1 转换成 word2 所使用的最少操作数 。

```
你可以对一个单词进行如下三种操作：
    插入一个字符
    删除一个字符
    替换一个字符
示例 1:
输入: word1 = "horse" , word2 = "ros"
输出: 3
解释:
    horse -> rorse (将 'h' 替换为 'r')
    rorse -> rose (删除 'r')
    rose -> ros (删除 'e')
```

#### 思路

这题做的我怀疑人生。我最开始想到的思路是：找出公共子序列，然后遍历一遍公共子序列，取子序列间距的较大值加起来。看了题解有点豁然开朗，觉得对DP的认识又深了一点。

状态：

状态转移方程：

#### 代码

```
    public int minDistance(String word1, String word2) {
        int[][] dp = new int[word1.length() + 1][word2.length() + 1];

        //预处理第一行和第一列
        for (int i = 0; i < word2.length() + 1; i++) {
            dp[0][i] = i;
        }
        for (int i = 0; i < word1.length() + 1; i++) {
            dp[i][0] = i;
        }

        for (int i = 1; i < word1.length() + 1; i++) {
            for (int j = 1; j < word2.length() + 1; j++) {
                //横着处理
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    int add = dp[i][j - 1] + 1;
                    int minus = dp[i - 1][j] + 1;
                    int modify = dp[i - 1][j - 1] + 1;
                    dp[i][j] = Math.min(Math.min(add, minus), modify);
                }
            }
        }
        return dp[word1.length()][word2.length()];
    }
```

### Leetcode198. 打家劫舍

#### 题目描述

你是一个专业的小偷，计划偷窃沿街的房屋。每间房内都藏有一定的现金，影响你偷窃的唯一制约因素就是相邻的房屋装有相互连通的防盗系统，如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警。

```
给定一个代表每个房屋存放金额的非负整数数组，计算你在不触动警报装置的情况下，能够偷窃到的最高金额。
示例 1:
输入: [1,2,3,1]
输出: 4
解释: 偷窃 1 号房屋 (金额 = 1) ，然后偷窃 3 号房屋 (金额 = 3)。
偷窃到的最高金额 = 1 + 3 = 4 。
```

