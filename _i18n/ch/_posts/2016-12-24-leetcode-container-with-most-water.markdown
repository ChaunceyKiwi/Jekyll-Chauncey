---
layout: post
title:  "Leetcode Question11: Container With Most Water"
date:   2016-12-24 11:40:42 -0700
categories: leetcode algorithm
---

# Question description:

Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container and n is at least 2.

# Disscusion:

通过穷举法可以得到一个解决方案：

{% highlight cpp %}
class Solution {
public:
  int maxArea(vector<int>& height) {
    int size = (int)height.size();
    int maxVolume = 0;
    
    for (int i = 0; i < size; i++) {
      for (int j = i + 1; j < size; j++) {
        while(j + 1 < size && height[j] < height[j+1]) {
          j++;
        }
        int h = min(height[i], height[j]);
        int volume = h * (j - i);
        if (volume > maxVolume) {
          maxVolume = volume;
        }
      }
    }
    return maxVolume;
  }
};

{% endhighlight %}

然而，作为中等难度的题目，仅仅是O(N^2)的时间复杂度算法几乎都会被卡在超时问题上。因为我们需要找到一个O(NlogN)或O(N) 的算法。

实际上当我做的时候我没能找到一个线性解。看了讨论区的答案以后，普遍的说法是在头尾放置i,j两个指针，通过向中间不断移动，并计算中间可能出现得最优解。我一开始即使看了答案也无法理解，不知道为什么这样做不会导致遗漏潜在的最优答案。

其实讨论区还是没有把这个问题最实质的地方讲出来。那就是在于这里的问题背景可以得出一个数学性质：每一个容器的高度是由它的左右两条边中较短的那一条决定的。倘若没有这个性质，这题应该就找不到一个O(n)的解。

正因为上面提到的这些性质，可以得到: 如果现在i,j都都处在某一位置并且i的高度小于j的高度，不管我们将j左移多少，都不能产生一个可以更优的容量。因为不管j怎么左移，边的高度上限是i的高度，并且宽度还在减小，因此面积只会更小，因此我们可以跳过这个情况，直接将i右移，而i右移是有可能产生更优解的。因此，只需比较两边的高，将较短边往中间移动即可。

另外一个优化则不是是由这个性质决定而是比较宽泛的。因为我们在收缩的过程中，宽度在缩短，因此高必须增加才有可能使面积增大。所以当指针往中部移动的时候，如果发现移动之后得到的边还不如一刚开始的长度，那么就继续往中部移动。代码如下:

{% highlight cpp %}
class Solution {
public:
  int maxArea(vector<int>& height) {
    int size = (int)height.size();
    int maxVolume = 0;
    int i = 0, j = size - 1;

    while (i <= j) {
      int h = min(height[i], height[j]);
      int volume = h * (j - i);
      if (volume > maxVolume) {
        maxVolume = volume;
      }
      while (height[i] <= h) {
        i++;
      }
      while (height[j] <= h) {
        j--;
      }
    }
    return maxVolume;
  }
};
{% endhighlight %}

感想：通过题目的描述，找到这一问题的特殊性质，并根据这一性质得到与之对应的优化，这样的思路对于解题会有比较大的帮助。

