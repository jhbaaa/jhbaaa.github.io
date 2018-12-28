---
layout: post
title: C++ 알고리즘 문제풀이용 알고리즘 - Merge Sort
date: 2018-12-28 11:52:00
category: algorithm
tag: [algorithm, c/c++, sort]
---
C++ 알고리즘 문제풀이용으로 작성한 Merge Sort 알고리즘이다.

합병 정렬(머지 소트) 이라고도 불린다.

```cpp
#define DATA_SIZE 10

void merge(int data[], int l, int r)
{
	int tmp[DATA_SIZE] = { 0, };
	int m = (l + r) / 2;
	int i = l;
	int j = m + 1;
	int k = l;

	// 작은 녀석 먼저 담음
	while (i <= m && j <= r)
	{
		if (data[i] < data[j])
			tmp[k++] = data[i++];
		else
			tmp[k++] = data[j++];
	}

	// 남은 것 담음
	while (i <= m) tmp[k++] = data[i++];
	while (j <= r) tmp[k++] = data[j++];

	for (i = l; i <= r; i++)
		data[i] = tmp[i];
}

void mergeSort(int data[], int l, int r)
{
	if (!(l < r))
		return;
	
	int m = (l + r) / 2;
	mergeSort(data, l, m);
	mergeSort(data, m + 1, r);
	merge(data, l, r);
}
```



사용은 아래와 같이 한다.

```cpp
#define DATA_SIZE 10

int data[DATA_SIZE] = { 3,6,2,8,1,9,6,2,13,-4 };

mergeSort(data, 0, DATA_SIZE - 1);

for (int i = 0; i < DATA_SIZE; i++)
{
	printf("%d ", data[i]);
}
```

