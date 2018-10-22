---
title: 数据结构模板之---RMQ
date: 2018-10-18 21:31:25
tags: 模板
---
由于本人太弱
所以现在才（zaojiu）会RMQ
所以不得不写个博客纪念
希望好评哦
下面贴代码
```cpp

#include <iostream>
#include <cstring>
#include <cmath>
#include <cstdio>
#include <cstdlib>
#include <cstdlib>
using namespace std;
int f[1000000][25];
int n;
int m;
int log1[3000000];
int main(){
    memset(f,0x3f3f3f3f,sizeof(f));
    cin>>n>>m;
    for(int i=1;i<=n;i++)
    {
        scanf("%d",&f[i][0]);
    }
    for(int j=1;j<=20;j++)
    {
        for(int i=1;i+(1<<j)-1<=n;i++)
        {
            f[i][j]=min(f[i][j-1],f[i+(1<<(j-1))][j-1]);
        }
    }
    while(m--)
    {
        int x,y;
        scanf("%d%d",&x,&y); 
        int wzx=log2(y-x+1);
        printf("%d ",min(f[x][wzx],f[y-(1<<wzx)+1][wzx]));
    }
    return 0;
}

```