---
layout : post
title : "Quick Sort Algorithm"
author : Jimmy Chen 
date : 2015-06-27 13:04:00
categories : jekyll update
---
Quick Sort is a widely used sort algorithm .

Here is the implement of c++

{% highlight c++ %}
void QuickSort(int a[] , int left , int right)
{
  if(left < right)
  {
      int key = a[left];
      int low = left;
      int high = right;
      while (low < high) {
          while(low < high && a[high] >= key)
          {
              high--;
          }
          a[low] = a[high];
          while(low < high && a[low] <= key)
          {
              low++;
          }
          a[high] = a[low];
      }
      a[low] = key;
      QuickSort(a, left, low - 1);
      QuickSort(a, low + 1 , right);
  }
}
#=> Sort the a[];
{% endhighlight %}
	