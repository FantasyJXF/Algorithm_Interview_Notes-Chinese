# 笔试面经

**回答一个面试问题的基本要点**

* 是什么、
* 为什么（动机）、
* 怎么做（原理）、
* 使用场景、
* 一些细节（如果使用过的话）

## Reference

* [BAT机器学习面试1000题系列（第1~305题）](https://blog.csdn.net/v_JULY_v/article/details/78121924) - CSDN博客 

## 笔试

* [字节跳动 180812](bi-shi-zi-jie-tiao-dong-180812.md)

## Index

* [头条/字节跳动-深度学习/NLP 方向](./#头条字节跳动-深度学习nlp-方向)
  * [一面](./#一面)
  * [二面](./#二面)
  * [三面](./#三面)
  * [四面（非加面）](./#四面非加面)
* [今日头条-算法工程师-实习](./#今日头条-算法工程师-实习)
  * [一面](./#一面-1)
  * [二面](./#二面-1)
  * [三面](./#三面-1)
* [2019 美团 AI - NLP 提前批](./#2019-美团-ai---nlp-提前批)
  * [一面（NLP平台）](./#一面nlp平台)
  * [一面（广告平台）](./#一面广告平台)
  * [二面（广告）](./#二面广告)
* [拼多多 180722 笔试](./#拼多多-180722-笔试)
  * [1. 数组中的最长山谷](./#1-数组中的最长山谷)
  * [2. 字符串构造](./#2-字符串构造)
  * [3. 到达指定位置](./#3-到达指定位置)
  * [4. 靓号](./#4-靓号)

## 头条/字节跳动-深度学习/NLP 方向

### 一面

* 自我介绍
* 聊项目
* 深度学习基本问题
* 【算法】手写 K-Means

  > 磕磕绊绊算是写出来一个框架，内部细节全是问题，面试官比较宽容，勉强算过了

### 二面

* 自我介绍
* 聊项目
* 深度学习基本问题
* 【算法】找数组中前 k 大的数字

  > 我说了两个思路：最小堆和快排中的 partition 方法；让我选一个实现，我选的堆方法，然后又让我实现调整堆的方法

### 三面

* 自我介绍
* 为什么会出现梯度消失和梯度爆炸
  * 分别说了下前馈网络和 RNN 出现梯度消失的情况
* 有哪些解决方法
  * 因为提到了残差和门机制，所以又问
  * 分别说下它们为什么能缓解梯度消失
  * 因为说残差的时候提到了 ResNet，让我介绍下 ResNet（没用过，随便说了几句）
* 其他加速网络收敛的方法（除了残差和门机制）
  * 我从优化方法的角度说了一点（SGB 的改进：动量方法、Adam）
  * 提示我 BN，然后我就把 BN 的做法说了一下
  * 然后问 BN 为什么能加速网络的收敛（从数据分布的角度随便说了几句）
* 传统的机器学习方法（简历上写用过 GBDT）
  * 简单介绍下 XGBoost
  * CART 树怎么选择切分点（基尼系数）
  * 基尼系数的动机、原理（不会）
* 【算法】直方图蓄水问题

  > LeetCode [42. 接雨水](https://leetcode-cn.com/problems/trapping-rain-water/description/)；
  >
  > > 当时太紧张没想出 `O(N)` 解法，面试一结束就想出来了，哎
  > >
  > > * 附 AC 代码
  > >
  > >   \`\`\`C++
  > >
  > >   class Solution {
  > >
  > >   public:
  > >
  > >   ```text
  > >   int trap(vector<int>& H) {
  > >       int n = H.size();
  > >   ```

  ```text
        vector<int> dp_fw(H);
        vector<int> dp_bw(H);

        for(int i=1; i<n; i++)      // 记录每个位置左边的最高点
            dp_fw[i] = max(dp_fw[i-1], dp_fw[i]);

        for(int i=n-2; i>=0; i--)   // 记录每个位置右边的最高点
            dp_bw[i] = max(dp_bw[i+1], dp_bw[i]);

        int ret = 0;
        for (int i=1; i<n-1; i++)  // 取两侧较矮的点
            ret += min(dp_fw[i], dp_bw[i]) - H[i];

        return ret;
    }
  ```

  };

  \`\`\`

### 四面（非加面）

> 因为流程出了问题，其实还是三面
>
> * 【算法】和为 K 的连续子数组，返回首尾位置
>
>   LeetCode [560. 和为K的子数组](https://leetcode-cn.com/problems/subarray-sum-equals-k/description/)
>
>   > 很熟悉的题，但就是没想出来；然后面试官降低了难度，数组改成有序且为正整数，用双指针勉强写了出来；但是边界判断有问题，被指了出来；然后又问无序的情况或者有负数的情况能不能也用双指针做，尬聊了几分钟，没说出个所以然。
>
> * 如何无监督的学习句子表示
>   * 我说 Self-Attention
>   * 让我把公式写出来，因为写的不清楚，让我写原始的 Attention
>   * 然后问怎么训练，损失函数是什么（没说出来，除了词向量我基本没碰过无监督任务，而且我认为词向量也算不上无监督...）
> * 如何无监督的学习一个短视频的特征表示
>   * 抽取关键帧，然后通过 ResNet 等模型对每一帧转化为特征表示，然后对各帧的特征向量做拼接或者直接保存为二维特征（瞎说的，别说视频，我连图像都没做过）

## 今日头条-算法工程师-实习

> [6.14今日头条算法工程师实习生](https://www.nowcoder.com/discuss/84462?type=2&order=0&pos=11&page=1)_笔经面经_牛客网

### 一面

1. 自我介绍；
2. 二分查找；

   > Algorithm\_for\_Interview/常用子函数/[二分查找模板.hpp](https://github.com/imhuay/Algorithm_for_Interview-Chinese/blob/master/Algorithm_for_Interview/_utils工具函数/二分查找模板.hpp)

3. 判断链表是否有环；

   > Algorithm\_for\_Interview/链表/[链表中环的入口结点.hpp](https://github.com/imhuay/Algorithm_for_Interview-Chinese/blob/master/Algorithm_for_Interview/链表/链表中环的入口结点.hpp)

4. 将数组元素划分成两部分，使两部分和的差最小，数组顺序可变；

   > Algorithm_for\_Interview/查找与排序/\[暴力搜索_划分数组使和之差最小.hpp\]\([https://github.com/imhuay/Algorithm\_for\_Interview-Chinese/blob/master/Algorithm\_for\_Interview/查找与排序/暴力搜索\_划分数组使和之差最小.hpp](https://github.com/imhuay/Algorithm_for_Interview-Chinese/blob/master/Algorithm_for_Interview/查找与排序/暴力搜索_划分数组使和之差最小.hpp)\)

5. 智力题，在一个圆环上随机添加3个点，三个点组成一个锐角三角形的概率；

   > ../数学问题/[\#1](https://github.com/FantasyJXF/Artificial-Intelligence/tree/9859473754e144ed8a6da363c7c773ac65a7a1a6/数学/README.md#1-在圆环上随机选取-3-个点这-3-个点组成锐角三角形的概率)

6. 推导逻辑斯蒂回归、线性支持向量机算法；

   > ../机器学习/[逻辑斯蒂回归推导](https://github.com/FantasyJXF/Artificial-Intelligence/tree/9859473754e144ed8a6da363c7c773ac65a7a1a6/机器学习/README.md#逻辑斯蒂回归推导)
   >
   > ../机器学习/[线性支持向量机推导](https://github.com/FantasyJXF/Artificial-Intelligence/tree/9859473754e144ed8a6da363c7c773ac65a7a1a6/机器学习/README.md#线性支持向量机推导)

### 二面

1. 在一个圆环上随机添加3点，三个点组成一个锐角三角形的概率；
2. 用积分计算上述概率；
3. 用程序解决上述问题

   > 多次采样求概率，关键是如何判断采样的三个点能否构成锐角三角形，不同的抽象会带来不同的复杂度。
   >
   > 最直接的想法是，根据边长关系，此时需要采样三个 x 坐标值，相应的 y 坐标通过计算得出，然后计算三边长度，再判断，循环以上过程，计算形成锐角的比例。
   >
   > 更简单的，根据 [../数学/\#1](https://github.com/FantasyJXF/Artificial-Intelligence/tree/9859473754e144ed8a6da363c7c773ac65a7a1a6/数学/README.md#1-在圆环上随机选取-3-个点这-3-个点组成锐角三角形的概率) 中提到的简单思路，原问题可以等价于“抛两次硬币，求两次均为正面的概率”——此时，只需要采样两个`(0, 1)`之间的值，当两个值都小于 0.5 意味着能构成锐角三角形。

4. 深度学习，推导反向传播算法，知道什么激活函数，不用激活函数会怎么样，ROC与precesion/recall评估模型的手段有何区别，什么情况下应该用哪一种？深度学习如何参数初始化？

   > ../深度学习/[反向传播算法](https://github.com/FantasyJXF/Artificial-Intelligence/tree/9859473754e144ed8a6da363c7c773ac65a7a1a6/深度学习/README.md#反向传播算法)
   >
   > ../深度学习/[激活函数](https://github.com/FantasyJXF/Artificial-Intelligence/tree/9859473754e144ed8a6da363c7c773ac65a7a1a6/深度学习/README.md#激活函数)
   >
   > ../深度学习/[参数初始化](https://github.com/FantasyJXF/Artificial-Intelligence/tree/9859473754e144ed8a6da363c7c773ac65a7a1a6/深度学习/README.md#参数初始化)

5. 介绍kaggle项目，titanic，用到了哪些框架，用到了哪些算法；

### 三面

1. 自我介绍；
2. 分层遍历二叉树，相邻层的遍历方向相反，如第一层从左到右遍历，下一层从右向左遍历；
3. 介绍AdaBoost算法；
4. 介绍梯度下降，随机梯度下降

   > ../深度学习/[梯度下降法](https://github.com/FantasyJXF/Artificial-Intelligence/tree/9859473754e144ed8a6da363c7c773ac65a7a1a6/深度学习/README.md#2-梯度下降法随机梯度下降)

5. 写出逻辑斯蒂回归的损失函数；
6. C++，虚函数，虚析构函数。

## 2019 美团 AI - NLP 提前批

> [2019美团AI算法提前批面试经验](https://www.nowcoder.com/discuss/85852?type=2&order=0&pos=7&page=1)_笔经面经_牛客网

### 一面（NLP平台）

**论文/项目相关**

* 意图识别数据怎么标注
* 怎么样做实体抽取
* 怎样进行 aspect-level 情感分析
* 模型中增强学习的 reward 如何设计的；为什么这样设计

### 一面（广告平台）

**论文/项目相关**

* seq2seq 中 scheduled sampling 如何做的
* RL部分训练过程中数据集如何构造
* 如何防止过拟合，你都采用了哪些方法，还有哪些你没有用到的方法

  > 深度学习/[正则化](https://github.com/FantasyJXF/Artificial-Intelligence/tree/9859473754e144ed8a6da363c7c773ac65a7a1a6/深度学习/README.md#正则化)

* 【**编程题**】给定整数n，求离根号n最近的整数。

  > [二分查找最优解模板](https://github.com/imhuay/Algorithm_for_Interview-Chinese/blob/master/Algorithm_for_Interview/_必背算法/二分查找最优解模板.hpp)

### 二面（广告）

**论文/项目相关**

* RL + Seq2seq相关问题
  * Seq2seq怎样和RL结合，这里的action与state都是什么
  * 如何设计reward，为什么选取这样的reward
  * 具体训练流程是怎样的

**深度学习相关**

* BiLSTM 相比 LSTM有哪些 case 上的提升
* Attention 是如何加的取得了哪些效果的提升
* 能介绍几个传统的机器学习模型吗，列举了：决策树，SVM, RF等
  * 具体说明一下决策树如何划分，写出相应的公式
  * 具体解释一下RF
* 【**编程题**】类似求一个旋转数组的拐点位置

  > 二分查找；[153. 寻找旋转排序数组中的最小值](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/description/) - LeetCode

## 拼多多 180722 笔试

共 4 道编程题

### 1. 数组中的最长山谷

> 问题描述：LeetCode 845. [数组中的最长山脉](https://leetcode-cn.com/problems/longest-mountain-in-array/description/)
>
> * 原题是找山脉，这里改成了山谷
>
>   ```text
>   示例：
>       输入：
>           [4,3,2,5,3,1,4,8]
>       输出：
>           5
>       说明：
>           [5,3,1,4,8]
>   ```
>
> * **“坑”点说明**
>   * 输入就是字符串 "\[4,3,2,5,3,1,4,8\]" 包括括号和标点
>   * 问题是，直接返回 0 也有 20% 的正确率，导致我一直没想到是输入上的问题，直到最后都卡在 20%
> * 建议所有需要处理字符串的问题，都使用 Python，这里只要 `A = eval(input())` 就完事了；而 C++ 如果不熟悉 STL 的话，处理输入都比题目本身难了
> * **思路**：暴力枚举；看代码更直观 
> * C++ 代码 [\[code\]](https://github.com/imhuay/Algorithm_for_Interview-Chinese/blob/master/Algorithm_for_Interview/_笔试/拼多多180722/1.数组中的最长山谷.hpp)（没做输入处理）

### 2. 字符串构造

* 问题描述

  ```text
  一个长串由一个字串循环构成，即 s[i]=t[i%n]，比如 "abcabc" 由 "abc" 构成

  注意："abcabcab" 也是由 "abc" 构成的，答题时没注意这个又只过了一部分

  *建议使用 Python 解决字符串相关问题
  ```

* **思路**：暴力枚举前缀
* Python 代码 [\[code\]](https://github.com/imhuay/Algorithm_for_Interview-Chinese/blob/master/Algorithm_for_Interview/_笔试/拼多多180722/2.字符串构造.py)

### 3. 到达指定位置

* 题目描述：Leetcode 754. [到达终点数字](https://leetcode-cn.com/problems/reach-a-number/description/)
* 数学题
* 思路：[一道乐视网的面试题，求解答？](https://www.zhihu.com/question/50790221/answer/125213696) - 知乎 
* C++ 代码 [\[code\]](https://github.com/imhuay/Algorithm_for_Interview-Chinese/blob/master/Algorithm_for_Interview/_笔试/拼多多180722/3.到达指定位置.hpp)

### 4. 靓号

* 问题描述

  ```text
  A 国的手机号码由且仅由 N 位十进制数(0-9)组成，可以有前导 0，比如 000123456。一个手机号码中至少有 K 位数相同则被定义为靓号（不要求连续）。
  如果想把自己的手机号修改为一个靓号，修改一个数字的金额为新数字与旧数字之间的差的绝对值，比如 1 修改为 6 或 6 修改为 1 都要花 5 块钱。
  求对给定手机号，修改为靓号最少要花的钱数以及新的号码（如果有多个，输出字典序最小的）。

  输入：
      第一行包含两个整数 N 和 K，分别表示 手机号码的位数和靓号要求的位数
      第二行为 N 个数字，数字之间没有空白符

      数据范围 2 <= K <= N <= 10000

  示例：
      输入：
          6 5
          785785
      输出：
          4
          777577
      说明: 777577 比 777775 字典序小
  ```

* **思路**：

  统计每个数字出现次数counter，以每个数字为基准，按照与基准差值对counter排序，优先替换差值小的数字；关于字典序的问题，如果替换的数比基准大则从前向后替换，如果替换的数比基准大，则从后向前替换，得到的就是字典序最小的字符串，时间复杂度O\(n\)

  > [拼多多算法岗笔试python解决方案](https://www.nowcoder.com/discuss/87694)_笔经面经_牛客网

* TODO 目前还没看到完全 AC 的代码
