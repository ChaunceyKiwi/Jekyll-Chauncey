---
layout: post
title: C++ Union 使用方法
date: 2016-05-16 02:11:28 -07:00
type: post
categories: programming
---
When I read c++ tutorial, I feel confused about the usage of c++ structure union. It looks like structure but every member elements occupy the same physical space in memory. So it can only store one values(But can be different types).

So with such a structure you can create a linked list whose nodes have different types of data just like the graph below illustrates:
!["Screen Shot 2016-05-15 at 7.09.08 PM.png"]({{ site.baseurl }}/assets/screen-shot-2016-05-15-at-7-09-08-pm.png)

Here are the code to demo:
{% highlight cpp %}
#include <iostream>
using namespace std;
union DataValue
{
	int v_int;
	float v_float;
	char* v_string;
};

struct DataNode
{
	DataValue value;
	DataNode *next;
};

int main(void)
{
	DataNode node1;
	DataNode node2;

	node1.value.v_int = 3;
	node2.value.v_string = "I am a string";
	node1.next = &node2;
	node2.next = NULL;

	DataNode *nodePtr = &node1;

	cout<<nodePtr->value.v_int<<endl;
	cout<<nodePtr->next->value.v_string<<endl;
}
{% endhighlight %}
