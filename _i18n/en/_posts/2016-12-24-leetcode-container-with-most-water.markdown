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

For sure it is easy to come up with a brute-force solution:

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

However, as a problem with difficulty as medium, it won't be such easy to pass. The time complexity is O(n^2), so we might need to find a solution with O(NlogN) or O(N).

Actually I failed when trying to find a linear solution. The reason in that is I cannot figure out why can we move the pointer linearly without leaving out some potential optimal situation.




