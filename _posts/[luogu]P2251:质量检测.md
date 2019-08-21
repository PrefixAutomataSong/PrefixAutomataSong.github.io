---
layout: post
title: "[luogu]P2251:质量检测"
date: 2019-08-21
category: 题解
---


## 刚刚学st表的我显得有些不知所措

昨天听什么树上倍增，LCA，听得津（~~亿~~）津（~~脸~~）有（~~懵~~）味（~~13~~）

就只有一个st表听得有点明白

初学st表的同学可以先做[这道题](https://www.luogu.org/problem/P3865)练练手

st表核心位置


```cpp
int pcm(int l,int r){
	int m=r-l+1;
	int w=log(m)/log(2);
	return max(f[l][w],f[r-(1<<w)+1][w]);
   //核心位置  按照题意可以将max换成min求最小值
}
```


-----------
进入正题，本题是一道st表的板子题

一直求 l-r的区间最小值即可

（P.S.:l=1,r=m）  随后l++,r++

当r=n时即可停止查询

话不多说上代码

```cpp
#include<bits/stdc++.h>
using namespace std;
int n,m,f[1000010][33],a[1000010],i,j; 
int pcm(int l,int r){
	int m=r-l+1;
	int w=log(m)/log(2);
	return min(f[l][w],f[r-(1<<w)+1][w]);
}
int main(){
	scanf("%d%d",&n,&m);
	for(int i=1;i<=n;i++){
	scanf("%d",&a[i]);
	f[i][0]=a[i];
	}
	for(j=1;j<=20;j++){
		for(i=1;i<=n;i++){
			if(i+(1<<j)-1<=n){
				f[i][j]=min(f[i][j-1],f[i+(1<<(j-1))][j-1]);
			}
		}
	}
	int l=1,r=m;
	while(r<=n)
	{
	printf("%d\n",pcm(l,r));
	l++;r++;
	}
	return 0;
}
```
