---
layout: post
title: C언어 알고리즘 대회용 Stack Class
date: 2018-12-27 23:39:00
category: [algorithm]
tag: [algorithm, c/c++, datastructure]
---
C언어 알고리즘 대회용 Stack Class이다.

STACK_MAX 값은 알아서 잘 바꿔줄 것

```cpp
#define STACK_MAX 100

template <typename T>
class Stack {

public:
	T data[STACK_MAX];
	int index;

	Stack() 
		:index(0) {}

	void Push(T val)
	{
		data[index++] = val;
	}

	T Pop()
	{
		T ret = data[--index];
		return ret;
	}

	int Empty()
	{
		if (index == 0)
			return 1;
		return 0;
	}

	int Full()
	{
		if (index == STACK_MAX)
			return 1;
		return 0;
	}
};
```



사용은 아래와 같이 한다.

```cpp
Stack<int> stack;

stack.Push(1);
stack.Push(2);
stack.Push(3);

while (!stack.Empty())
{
	printf("%d ", stack.Pop());
}
```

