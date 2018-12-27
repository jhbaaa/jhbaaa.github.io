---
layout: post
title: C++ 알고리즘 문제풀이용 자료구조 - Heap
date: 2018-12-28 01:50:00
category: algorithm
tag: [algorithm, c/c++, datastructure]
---
C++ 알고리즘 문제풀이용으로 작성한 Heap Class다.

빠른 속도를 위해 배열로 짰고, Min, Max Heap 둘다 지원 한다.

```cpp
#define HEAP_MAX 1000
#define ERR 0x7fffffff

inline void swap(int *a, int *b)
{
	int tmp = *a;
	*a = *b;
	*b = tmp;
}

typedef bool(*CmpFuncT)(int, int);

bool CmpMin(int l, int r)
{
	return l < r;
}

bool CmpMax(int l, int r)
{
	return l > r;
}

class Heap
{
public:
	CmpFuncT Compare = CmpMin;
	int index = 0;
	int data[HEAP_MAX] = { 0, };

	Heap() {}
	Heap(bool maxheap)
	{
		Heap();
		if (maxheap)
			Compare = CmpMax;
	}

	void put(int val)
	{
		index++;
		data[index] = val;
		int c = index;
		int p = index / 2;
		
		//while (p >= 1 && data[c] < data[p])
		while (p >= 1 && Compare(data[c], data[p]))
		{
			swap(&data[c], &data[p]);
			c = p;
			p = c / 2;
		}
	}

	int pop()
	{
		if (index == 0)
			return ERR;
		int ret = data[1];
		swap(&data[1], &data[index]);
		index--; // pop 된 녀석 제외 시킨다

		int p = 1;
		int c = p * 2;

		while (c <= index)
		{
			// 포인트는 c < index 인 것과 우측놈만 보는 것
			//if (c < index && data[c + 1] < data[c])
			if (c < index && Compare(data[c + 1], data[c]))
				c++;
			//if (data[c] >= data[p])
			if (!Compare(data[c], data[p]))
				break;
			swap(&data[p], &data[c]);
			p = c;
			c = 2 * p;
		}
		return ret;
	}	
};
```



사용은 아래와 같이 한다.

```cpp
Heap heap(true);
heap.put(3);
heap.put(6);
heap.put(2);
heap.put(8);
heap.put(5);
heap.put(3);
heap.put(9);

int c;
while ((c = heap.pop()) != ERR)
{
	printf("%d ", c);
}
```

