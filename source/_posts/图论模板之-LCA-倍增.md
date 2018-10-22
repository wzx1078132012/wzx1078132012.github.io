---
title: 图论模板之--LCA(倍增)
date: 2018-10-22 18:43:52
tags: 模板
---
LCA倍增模板（非常拙劣）
```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <cmath>
using namespace std;
int n,m,s;
int next[5000005],head[5000005],to[5000005];
int dis[5000005],f[1000005][25];
int cnt=0;
int add(int x,int y)
{
    next[++cnt]=head[x];
    head[x]=cnt;
    to[cnt]=y;
}
void dfs(int x,int father)
{
    dis[x]=dis[father]+1;
    for(int i=0;i<=19;i++)
    {
        f[x][i+1]=f[f[x][i]][i];
    }
    for(int i=head[x];i;i=next[i])
    {
        int wzx=to[i];
        if(wzx!=father)
        {
            f[wzx][0]=x;
            dfs(wzx,x);
        }
        else
        continue;
    }
}
int lca(int x,int y)
{
    if(dis[y]>dis[x])
    swap(y,x);
    for(int i=20;i>=0;i--)
    {
        if(dis[f[x][i]]>=dis[y])
        x=f[x][i];
        if(y==x)
        return x;
    }
    for(int i=20;i>=0;i--)
    {
        if(f[x][i]!=f[y][i])
        {
            x=f[x][i];
            y=f[y][i];
        }
    }
    return f[x][0];
}
int main(){
    int x,y;
    cin>>n>>m>>s;
    n--;
    while(n--)
    {
        cin>>x>>y;
        add(x,y);
        add(y,x);
    }
    dfs(s,0);
    while(m--)
    {
        scanf("%d%d",&x,&y);
        printf("%d\n",lca(x,y));
    }
    return 0;
}

```
