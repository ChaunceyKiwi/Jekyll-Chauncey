---
layout: post
title: C++ Enum 使用方法
date: 2016-05-16 03:05:14.000000000 -07:00
type: post
published: true
status: publish
categories: programming
tags: cpp
---
With enumerator we do not need to remember the correspondence between the number and the object it refer to. In CG programming, we usually need a lot of object to draw, which have its VAO and VBO. When there are too many object we have to look back at code to find the correspondence. Here we can use enumerator to save time.

{% highlight cpp %}
#include <iostream>
#include <string>
using namespace std;
enum objectType{
	Grid,
	Board,
	Tile,
	numOfObject
};

int main(void)
{
	string VBO[numOfObject];
	VBO[Grid] = "I am grid";
	VBO[Board] = "I am board";
	VBO[Tile] = "I am tile";

	cout<<VBO[Grid]<<endl;
	cout<<VBO[Board]<<endl;
	cout<<VBO[Tile]<<endl;
}

{% endhighlight %}

And another usage is that you can use it in the condition sentence case now.
{% highlight cpp %}
void printDataNode(DataNode* ptr)
{
	printf("I am a ");
	switch(ptr->type){
	case INTEGER: printf("Integer with value %d", ptr->value.v_int); break;
	case FLOAT_POINT: printf("Float with value %f", ptr->value.v_float); break;
	case STRING: printf("String with value %s", ptr->value.v_string); break;
}
{% endhighlight %}
