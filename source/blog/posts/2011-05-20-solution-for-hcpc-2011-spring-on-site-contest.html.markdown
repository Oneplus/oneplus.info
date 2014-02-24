---
layout: post
status: publish
published: true
title: HCPC 2011 Spring On-Site Contest 解题报告
author: Oneplus
author_login: oneplus
author_email: oneplus.lau@gmail.com
author_url: http://blog.oneplus.info
excerpt: ! "在解题报告的最前面，要对<a href=\"http://blog.oneplus.info/archives/230\">上一篇</a>的中一句很不负责任的评论表达十分的歉意。出现这样的失误，完全是我没有认真组织题目校验，对于命题人投的题没有合理组织照成版本混乱，传达要求不清晰明确造成的。以后不管是我还是范利鑫，都要注意避免这样的问题发生。\r\n"
wordpress_id: 283
wordpress_url: http://blog.oneplus.info/?p=283
date: 2011-05-20 05:20:16.000000000 +08:00
categories:
- 可以控制
- HIT ACM/ICPC Group
tags:
- ACM Group
- HCPC 2011 Spring
comments:
- id: 134
  author: Lambyy
  author_email: lambyy@hit.edu.cn
  author_url: ''
  date: !binary |-
    MjAxMS0wNS0yMCAxMTo1MDoyOCArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wNS0yMCAwMzo1MDoyOCArMDgwMA==
  content: 一佳神辛苦了~
- id: 137
  author: Lancelot
  author_email: lycanlancelot@gmail.com
  author_url: http://NONE
  date: !binary |-
    MjAxMS0wNS0yMSAwODowOTo0MiArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wNS0yMSAwMDowOTo0MiArMDgwMA==
  content: 一佳学长辛苦了，后生可畏啊~~
- id: 138
  author: cot
  author_email: lzbshen@sina.com
  author_url: ''
  date: !binary |-
    MjAxMS0wNS0yMSAxMToxODowMCArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wNS0yMSAwMzoxODowMCArMDgwMA==
  content: 排名第二的同学威武啊
- id: 139
  author: wangqinshi
  author_email: wangqinshi1995@gmail.com
  author_url: ''
  date: !binary |-
    MjAxMS0wNS0yMSAxODo1NTowNCArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wNS0yMSAxMDo1NTowNCArMDgwMA==
  content: ! "G题怎么求的f(i)没懂。\r\n我的做法是二分，每次计算序列中<=a1/b1的数的个数，计算方法是枚举b，然后统计有多少个a使得a/b
    <= a1/b1即1..(b*a1/b1)中有多少个数与b互质，这个问题是NOI2010energy的核心子问题，解法是容斥，直到<=a1/b1的数恰好有k个。然后枚举一下分母，找到a/b，然后再枚举分母，找到逼近的上下界。\r\nP.S.
    我是那个第二，希望把这个加到题解里"
- id: 140
  author: wangqinshi
  author_email: wangqinshi1995@gmail.com
  author_url: ''
  date: !binary |-
    MjAxMS0wNS0yMSAxOToxMzoyNSArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wNS0yMSAxMToxMzoyNSArMDgwMA==
  content: D题没有说cost[i]不降吧
- id: 141
  author: wangqinshi
  author_email: wangqinshi1995@gmail.com
  author_url: ''
  date: !binary |-
    MjAxMS0wNS0yMSAxOToxNDoyNyArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wNS0yMSAxMToxNDoyNyArMDgwMA==
  content: 我是说f[i]，错了
- id: 142
  author: wywcgs
  author_email: wywcgs@gmail.com
  author_url: ''
  date: !binary |-
    MjAxMS0wNS0yMiAxODo1Mjo1MCArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wNS0yMiAxMDo1Mjo1MCArMDgwMA==
  content: ! "确实够威武……\r\n现在的小孩子们都太可怕了……"
- id: 146
  author: ronaflx
  author_email: 900831flx@gmail.com
  author_url: ''
  date: !binary |-
    MjAxMS0wNS0yNyAyMTo1MzowNyArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wNS0yNyAxMzo1MzowNyArMDgwMA==
  content: 求把我的名字，打上马赛克学长……在博客上还是用我的ID吧，不要把我真实姓名暴露出来呀
- id: 935
  author: Amberly
  author_email: 313620018@qq.com
  author_url: http://www.facebook.com/
  date: !binary |-
    MjAxMi0wOS0xMyAwOToxODoyNSArMDgwMA==
  date_gmt: !binary |-
    MjAxMi0wOS0xMyAwMToxODoyNSArMDgwMA==
  content: That kind of thiinkng shows you're on top of your game
---

在解题报告的最前面，要对<a href="http://blog.oneplus.info/archives/230">上一篇</a>的中一句很不负责任的评论表达十分的歉意。出现这样的失误，完全是我没有认真组织题目校验，对于命题人投的题没有合理组织照成版本混乱，传达要求不清晰明确造成的。以后不管是我还是范利鑫，都要注意避免这样的问题发生。

<div>_____________________________解题报告分割线_____________________________</div>

网络赛C题的解题报告已经更新，想看的同学请移步<a href="http://blog.oneplus.info/archives/230#target">这里</a>

<div>_____________________________解题报告分割线_____________________________</div>

赛前草草的测试赛中，70学长给出的各题目难度分布如下（感谢70）：

<table width="100%">
<tr style="background:#eee"><th>Pid</th><th>Title</th><th>Author</th><th>Category</th><th>Expected Difficulty(5)</th></tr>
<tr><td><a href="http://acm.hit.edu.cn/judge/show.php?Proid=3024">A</a></td>
<td>Best Fit Ring</td><td>jerrybond</td><td>线段树DP</td><td>3</td></tr>
<tr><td><a href="http://acm.hit.edu.cn/judge/show.php?Proid=3025">B</a></td>
<td>Seven Road</td><td>Darkgt</td><td>随机化几何</td><td>3.5</td></tr>
<tr><td><a href="http://acm.hit.edu.cn/judge/show.php?Proid=3026">C</a></td>
<td>Shortest Path</td><td>Darkgt</td><td>贪心</td><td>3</td></tr>
<tr><td><a href="http://acm.hit.edu.cn/judge/show.php?Proid=3027">D</a></td>
<td>Power-supply System</td><td>Xnozero</td><td>BCC缩点、树DP</td><td>5</td></tr>
<tr><td><a href="http://acm.hit.edu.cn/judge/show.php?Proid=3028">E</a></td>
<td>Play Beans Beans</td><td>Lambyy</td><td>模拟</td><td>1.5</td></tr>
<tr><td><a href="http://acm.hit.edu.cn/judge/show.php?Proid=3029">F</a></td>
<td>Dictionary</td><td>yangjing</td><td>模拟</td><td>1</td></tr>
<tr><td><a href="http://acm.hit.edu.cn/judge/show.php?Proid=3030">G</a></td>
<td>Find the Fraction</td><td>Lambyy</td><td>分数序列、分数逼近</td><td>5++</td></tr>
<tr><td><a href="#">H</a></td>
<td>Rectangular Grid</td><td>SRM 146</td><td>水</td><td>0.5</td></tr>
<tr><td><a href="http://acm.hit.edu.cn/judge/show.php?Proid=3023">I</a></td>
<td>Zero Pair</td><td>Xnozero</td><td>Hash、模逆元</td><td>3</td></tr>
</table>

赛前本来计划把Zero Pair放到A。这样，Power-supply System就自然被放到E的位置，Lambyy的模拟题也就不会造成这么多误会。但是在插数据表时被我脑残把I查到网络赛最后一题的位置了。（恩，没错，就是数据库pid一项出现重复，而且pid居然不是主键却又好像是Status表的外键，额…HOJ的数据库设计）结果就变成了Lambyy的水题都被大家当成难题了。另一件自我批评的是，整个比赛中出现：H数据范围不明，I题input错（后来证实是Zero把新题面给我但我没改），A的Sample错，D的Sample错，C的时限错。╮(╯_╰)╭

<div>_____________________________解题报告分割线_____________________________</div>

#### Best Fit Ring

*[by jerrybond]* 计算各点到中心的距离，按距离大小将点排序，合并距离相等的点。问题转化为最大子段和问题。由于本题有动态更新每点的值，普通动态规划解决这个问题的复杂度为<em>O(QC<sup>2</sup>)</em>，对于本题数据范围不适用。需要线段树进行维护。

~~~cpp 
#include<math.h>
#include<stdio.h>
#include<string.h>
#include<stdlib.h>

#define Max(x, y) (x)>(y)?(x):(y)

struct Point {
    int x, y, v;
    int dis;
    int id;
}pt[100001];

struct Node {
    int l, r, sum, maxl, maxr, max;
}node[400001], ans;

int id[100001], tot, p[100001];

void save(int s) {
    int l = s<<1, r = (s<<1) + 1;
    node[s].sum = node[l].sum + node[r].sum;
    node[s].maxl = Max(node[l].maxl, node[l].sum + node[r].maxl);
    node[s].maxr = Max(node[r].maxr, node[r].sum + node[l].maxr);
    node[s].max = node[l].maxr + node[r].maxl;
    node[s].max = Max(node[s].max, node[l].max);
    node[s].max = Max(node[s].max, node[r].max);
}

void build(int l, int r, int s) {
    node[s].l = l;
    node[s].r = r;
    if (l == r) {
        node[s].sum = node[s].max = node[s].maxl = node[s].maxr = pt[l].v;
        return;
    } else if (r > l) {
        int mid = (l + r)>>1;
        build(l, mid, s<<1);
        build(mid+1,r, (s<<1)+1);
        save(s);
    }
}

void insert(int l, int r, int s, int v) {
    if (l == node[s].l & node[s].r == r) {
        node[s].sum = node[s].max = node[s].maxl = node[s].maxr = v;
        return;
    } else if (node[s].r > node[s].l) {
        int mid = (node[s].r + node[s].l)>>1;
        if (r <= mid) insert(l,r,s<<1,v);
        else if (l > mid) insert(l,r,(s<<1)+1,v);
        else {
            insert(l, mid, s<<1, v);
            insert(mid+1, r, (s<<1)+1, v);
        }
        save(s);
    }
}

struct Node check(int l, int r, int s) {
    if (l == node[s].l & node[s].r == r)
        return node[s];
    int mid = (node[s].l + node[s].r)>>1;
    if (r <= mid) return check(l, r, s<<1);
    else if (l > mid) return check(l, r, (s<<1)+1);
    else {
        struct Node tmp, lt, rt;
        lt = check(l, mid, s<<1);
        rt = check(mid+1, r, (s<<1)+1);
        tmp.sum = lt.sum + rt.sum;
        tmp.maxl = Max(lt.maxl, lt.sum+rt.maxl);
        tmp.maxr = Max(rt.maxr, rt.sum+lt.maxr);
        tmp.max = lt.maxr + rt.maxl;
        tmp.max = Max(tmp.max, lt.max);
        tmp.max = Max(tmp.max, rt.max);
        return tmp;
    }
}

int cmp(const void*p1, const void*p2) {
    struct Point*a1 = (struct Point*)p1;
    struct Point*a2 = (struct Point*)p2;
    if (a1->dis<a2->dis) return -1;
    else if (a1->dis==a2->dis) return 0;
    else return 1;
}

int main(void) {
    int n, m, i, j, d, x;
    char str[10];

    while (scanf("%d", n)==1) {
        for (i=1;i<=n;i++) {
            scanf("%d %d %d",pt[i].x,&pt[i].y,&pt[i].v);
            pt[i].dis=pt[i].x*pt[i].x + pt[i].y*pt[i].y;
            pt[i].id=i;
            p[i]=pt[i].v;
        }

        qsort(pt+1, n, sizeof(struct Point), cmp);

        j=n;
        tot=1;
        id[pt[1].id]=1;
        for (i=2;i<=j;i++) {
            if (pt[i].dis!=pt[i-1].dis)
                pt[++tot]=pt[i];
            else pt[tot].v+=pt[i].v;
            id[pt[i].id]=tot;
        }

        build(1,tot,1);
        scanf("%d", m);
        for (i=1;i<=m;i++) {
            scanf("%s", str);
            if (str[0]=='C') {
                scanf ("%d %d", d, &x);
                pt[id[d]].v=pt[id[d]].v-p[d]+x;
                p[d]=x;
                insert(id[d],id[d],1, pt[id[d]].v);
            } else {
                ans = check(1,tot,1);
                printf ("%d\n", ans.max);
            }
        }
    }
    return 0;
}
~~~

#### Seven Roads

<strong>[by Darkgt]</strong>此题是求平面点中共线最多的点数，对于一般的情况需要O(n<sup>2</sup>logn)的复杂度，枚举一个点需要O(n)复杂度，验证需要O(nlogn)。

此题明确所有的点最多只在7条直线上，因此如果随机选取一个点有大于1/7的概率取到最多点数的直线，如果每组数据只随机取30个点用来验证，在最坏的情况下有(6/7)<sup>30</sup>&le;1%的概率算法错误，由于最多只有30组数据，理论上可以跑对全部数据。当然，适当增加或减小枚举的点数，可以影响程序的正确率和速度。

~~~cpp 
#include <stdio.h>
#include <algorithm>
#include <iostream>
#include <cmath>
#include <ctime>
using namespace std;
struct tt
{
    int x;
    int y;
} a[10001];
bool cmp(const ttb,const tt&c)
{
    if(b.x==c.x) return b.y < c.y;
    return b.x < c.x;
}
double d[10001];
double INF = 1000000000.0;
double eps = 1e-8;
int cal(int n)
{
    int i,j,ans,k,max;
    if(n<3) return n;
    ans = 1;
    int cnt=30;
    srand((unsigned) time(NULL));
    while(cnt--)
    {
        i=rand()%n;
        k = 0;
        for(j = 0; j < n; j++)
        {
            if(i==j) continue;
            if(a[i].x==a[j].x)
                d[k] = INF;
            else
                d[k] = double(a[i].y - a[j].y) / (a[i].x - a[j].x);
            k++;
        }
        sort(d,d+k);
        max = 2;
        for(j = 1; j < k; j++)
        {
            if(fabs(d[j]-d[j-1])<eps )
                max++;
            else
            {
                if(max > ans)
                    ans = max;
                max = 2;
            }
        }
        if(max > ans)
            ans = max;
    }
    if(ans<n/7) while(1);
    return ans;
}
int main()
{
    int n,ca;
    scanf("%d",ca);
    while(ca--)
    {
        scanf("%d",n);
        for(int i = 0; i < n; i++)
            scanf("%d%d",a[i].x,&a[i].y);
        int ans=cal(n);

        printf("%d\n",ans);
    }
    return 0;
}
~~~

#### Shortest Path

<strong>[by Darkgt]</strong>如果用s[i]表示到达第i个位置所需最少步数，可以发现s[i-1]&le;s[i]，具有dp的性质，但dp的复杂度无法解决此题。发现s[i]=p的位置是连续的并且由s[i]=p-1的位置转移到，于是每次可以转移s值相等的一个区间，复杂度O(n)。

~~~cpp 
#include <cstdio>
#include <algorithm>
using namespace std;
const int M = 100005;
int x[M];
int n;
int main()
{
    int ca;
    scanf("%d",ca);
    while(ca--){
        scanf("%d",n);
        for(int i=0;i<n;i++)
            scanf("%d",x[i]);
        int left=0,right=1,nextright,ans;
        for(ans=0;;ans++){
            if(right<=left) {
                ans=-1;
                break;
            }
            if(left<=n-1&n-1<right) break;
            nextright=-1;
            for(int i=left;i<right;i++)
                nextright=max(nextright,i+x[i]+1);
            left=right;
            right=nextright;
        }
        printf("%d\n",ans);
    }
    return 0;
}
~~~

#### Power-supply System

<strong>[by sevenzero]</strong>这题我和Xnozero合出来防AK的，题目是从CF64的E改的，原题是个n<sup>3</sup>的树DP，我想了n<sup>2</sup>的办法于是将原题数据改大了，考虑到刷刷的存在，为了增加难度就加了双连通分量的缩点，好吧，已经基本不可做了。

先缩点，不会的自己去学，值得一提的是双连通分量的缩点分为基于割和基于桥的两种，本来想出基于割的缩点（参考2010杭州regional的G），最后自己都觉得太恶心就换成基于桥的缩点了。

DP部分要用3个数组in、out、inm。
<ul><li>in[i][j]为以i为根的子树中有发电站给i供电且与i的距离为j的最小花费，</li>
<li>inm[i]=min(in[i][j]) 辅助数组，</li>
<li>out[i][j]为以i为根的子树外有发电站给i供电且与i的距离为j或者在子树内有发电站给i供电的最小花费。</li></ul>

对于in[i][j]:
<ul><li>j=0时，说明就在i点建站，in[i][j]=sigma(out[son(i).k][j+1])+cost[i];</li>
<li>j>0时，说明发电站来自i的某儿子在的子树，对于这个子树来说发电站在这个子树里，其他子树来说在发电站子树外，</li></ul>
故方程有`in[i][j]=min(sigma(out[son(i).k][j+1])+in[son(i).k][j-1]-out[son(i).k][j+1]+f[j]),<br />sigma(out[son(i).k][j+1])`可以提前算出作为常数使用，故这里也只用一重循环就可解决，保证最后算法是n<sup>2</sup>的复杂度。
`out[i][j]=min(sigma(out[son(i).k][j+1])+f[j],inm[i])。`
inm[root]即为最终答案，整个过程可以用记忆化搜索实现。

~~~cpp 

#include <vector>
#include <list>
#include <map>
#include <set>
#include <deque>
#include <stack>
#include <bitset>
#include <algorithm>
#include <functional>
#include <numeric>
#include <utility>
#include <sstream>
#include <iostream>
#include <iomanip>
#include <cstdio>
#include <cmath>
#include <cstdlib>
#include <ctime>
#include <cstring>

using namespace std;

#define V 1011
#define E 1000001

int dfn[V], order, anc[V], bridge[V], stk[V], top, cntb, bcc[V], cntbcc;

struct ED
{
    int v;
    ED *next;
} pool[E], *base[V], *topp;

void init()
{
    topp = pool;
    memset(base, 0, sizeof (base));
}

void addedge(int i, int j)
{
    topp->v = j;
    topp->next = base[i];
    base[i] = topp++;
}

bool vis[V], vise[E];

void dfs(int i)
{
    dfn[i] = order++;
    vis[i]=1;
    anc[i] = i;
    stk[top++]=i;
    for (ED *ip = base[i]; ip != NULL; ip = ip->next)
    {
        int j = ip->v;
        if (vis[j])
        {
            if (!vise[ip - pool] & dfn[anc[i]] > dfn[j])
                anc[i] = j;
        }
        else
        {
            vise[ip - pool] = 1;
            vise[(ip - pool)^1] = 1;
            dfs(j);
            if (dfn[anc[i]] > dfn[anc[j]])
                anc[i] = anc[j];
            if (j == anc[j])
            {
                bridge[cntb++] = ip - pool;
                do
                {
                    bcc[stk[--top]]=cntbcc;
                }while(stk[top]!=j);
                cntbcc++;
            }
        }
    }
}
// BCCs are indexed from 0 to cntbcc-1 , bridges are indexed from 0 to cntb-1
void bridge_bcc(int n)
{
    memset(vis, 0, sizeof (vis));
    memset(vise, 0, sizeof (vise));
    cntb = 0;
    cntbcc=0;
    for (int i = 0; i < n; i++)
        if (!vis[i])
        {
            top=0;
            order = 0;
            dfs(i);
            while(top)
                bcc[stk[--top]]=cntbcc;
            cntbcc++;
        }
}

vector<int> ed[V];
int c,d[V],cost[V];
int in[V][V],inm[V],out[V][V];
bool vm[V]={0},vi[V][V]={0},vo[V][V]={0};
int inf(int,int,int);
int inmf(int,int);
int outf(int,int,int);

int inmf(int x,int f)
{
    if(vm[x])
        return inm[x];
    for(int i=0;i<cntbcc;i++)
        if(inm[x]>inf(x,i,f))
        {
            inm[x]=inf(x,i,f);
        }
    vm[x]=1;
    return inm[x];
}

int inf(int i,int j,int f)
{
    if(vi[i][j]) return in[i][j];
    vi[i][j]=1;
    int ret=0;
    for(int k=0;k<ed[i].size();k++)
        if(ed[i][k]!=f)
            ret+=outf(ed[i][k],j+1,i);
    if(!j)
        return in[i][j]=ret+cost[i];
    for(int k=0;k<ed[i].size();k++)
        if(ed[i][k]!=f)
            in[i][j]=min(in[i][j],ret+inf(ed[i][k],j-1,i)-outf(ed[i][k],j+1,i)+d[j]);
    return in[i][j];
}

int outf(int i,int j,int f)
{
    if(j>=cntbcc) return outf(i,cntbcc-1,f);
    if(vo[i][j]) return out[i][j];
    vo[i][j]=1;
    int ret=d[j];
    for(int k=0;k<ed[i].size();k++)
        if(ed[i][k]!=f)
            ret+=outf(ed[i][k],j+1,i);
    out[i][j]=min(inmf(i,f),ret);
    return out[i][j];
}

bool mtx[V][V];
int main()
{
    int n,m;
    while(scanf("%d%d%d",n,&m,&c)!=EOF)
    {
        init();
        int a,b;
        for(int i=0;i<m;i++)
        {
            scanf("%d%d",a,&b);
            addedge(a-1,b-1);
            addedge(b-1,a-1);
        }
        for(int i=0;i<n-1;i++)
            scanf("%d",d[i+1]);
        bridge_bcc(n);
        for(int i=0;i<cntbcc;i++) cost[i] = c;
        memset(mtx,0,sizeof(mtx));
        for(int i=0;i<n;i++)
        {
            cost[bcc[i]]++;
            for(ED *ip=base[i];ip;ip=ip->next)
                if(bcc[i]!=bcc[ip->v])
                    mtx[bcc[i]][bcc[ip->v]]=mtx[bcc[ip->v]][bcc[i]]=1;
        }
        for(int i=0;i<n;i++) ed[i].clear();
        for(int i=0;i<cntbcc;i++)
            for(int j=i+1;j<cntbcc;j++)
                if(mtx[i][j])
                {
                    ed[i].push_back(j);
                    ed[j].push_back(i);
                }
        memset(in,0x3f,sizeof(in));
        memset(inm,0x3f,sizeof(inm));
        memset(out,0x3f,sizeof(out));
        memset(vm,0,sizeof(vm));
        memset(vi,0,sizeof(vi));
        memset(vo,0,sizeof(vo));
        printf("%d\n",inmf(0,0));
    }
    return 0;
}
~~~

#### Play Beans Beans

<strong>[by Lambyy]</strong>水题一枚, 题意可能比较绕, 但自认为题意描述很清楚, 基本按题意模拟下来即可, 第一组Sample 数据即蕴含了本题最大的Trick, 即在每一个Round过程中新产生的空白点, 是不会被进行操作的, 否则Sample就得7了, 相信大部分过了的人都考虑到了这种情况.
定位为简单模拟题, 基本全场题, 没想卡人……

~~~cpp 
#include <cstdio>
#include <cstring>
const int N = 32;

int flag, w, h;
char map[N][N];
bool f[N][N];

int up (int x, int y, int t) {
    for (int i = x - 1; i >= 0; i--) {
        if (map[i][y] != '.') {
            t = x - i;
            return (map[i][y] - 'A');
        }
    }
    return -1;
}

int down (int x, int y, int t) {
    for (int i = x + 1; i < h; i++) {
        if (map[i][y] != '.') {
            t = i - x;
            return (map[i][y] - 'A');
        }
    }
    return -2;
}

int left (int x, int y, int t) {
    for (int i = y - 1; i >= 0; i--) {
        if (map[x][i] != '.') {
            t = y - i;
            return (map[x][i] - 'A');
        }
    }
    return -3;
}

int right (int x, int y, int t) {
    for (int i = y + 1; i < w; i++) {
        if (map[x][i] != '.') {
            t = i - y;
            return (map[x][i] - 'A');
        }
    }
    return -4;
}

void solve() {
    int i, j, t = 0;
    int t1, t2, t3, t4, x1, x2, x3, x4;
    for (i = 0; i < h; i++) {
        for (j = 0; j < w; j++) {
            f[i][j] = (map[i][j] == '.');
        }
    }

    for (i = 0; i < h; i++) {
        for (j = 0; j < w; j++) {
            t1 = t2 = t3 = t4 = -5;
            x1 = x2 = x3 = x4 = 0;
            if (f[i][j]) {
                t1 = up(i, j, x1);
                t2 = down(i, j, x2);
                t3 = left(i, j, x3);
                t4 = right(i, j, x4);
                if (t1 == t2) {
                    t = 1;
                    map[i - x1][j] = '.';
                    map[i + x2][j] = '.';
                }
                if (t1 == t3) {
                    t = 1;
                    map[i - x1][j] = '.';
                    map[i][j - x3] = '.';
                }

                if (t1 == t4) {
                    t = 1;
                    map[i - x1][j] = '.';
                    map[i][j + x4] = '.';
                }

                if (t2 == t3) {
                    t = 1;
                    map[i + x2][j] = '.';
                    map[i][j - x3] = '.';
                }

                if (t2 == t4) {
                    t = 1;
                    map[i + x2][j] = '.';
                    map[i][j + x4] = '.';
                }

                if (t3 == t4) {
                    t = 1;
                    map[i][j - x3] = '.';
                    map[i][j + x4] = '.';
                }
            }
        }
    }
    if (t == 0) {
        flag = 1;
        return;
    }
    solve();
    return;
}

int main() {
    int i, j, cnt;
    while (scanf("%d %d", h, &w) == 2 && w + h) {
        for (i = 0; i < h; i++) scanf("%s", map[i]);

        flag = cnt = 0;
        solve();
        for (i = 0; i < h; i++)
            for (j = 0; j < w; j++)
                cnt += (map[i][j] == '.');
        printf("%d\n", w * h - cnt);
    }
    return 0;
}
~~~

#### Dictionary

处理XML，求到行首距离为Q的标签的属性。可以一边读入一边递归着求。也可以都读入后去掉正文，再递归处理，总之是递归着做，比较简单。校验时觉得属性名有空格太坑又没什么意思，就把有空格的数据去掉。

~~~cpp 
#include <iostream>
#include <sstream>
#include <cstring>
#include <vector>
using namespace std;

vector<string> S, res;
int tag;
void dfs(int sum, int now) {
    if(now == S.size())
        return;
    string tmp = S[now];
    for( int i = 0; i < tmp.size(); i ++ )
        if( tmp[i] == '<' || tmp[i] == '>' || tmp[i] == ',' ) tmp[i] = ' ';
    stringstream SS(tmp); string name; int len; SS >> name >> len;
    if(sum + len == tag){ res.push_back(name); }
    while(1){
        tmp = S[++ now];
        if(tmp[1] == '/') break;
        else dfs(sum + len, now);
    }
}

int main() {
    int n, m;
    while( scanf( "%d%d", n, &tag ) == 2 ) {
        string buf;
        getchar(); S.clear(); res.clear();
        for( int i = 0; i < n; i ++ ) {
            getline( cin, buf );
            if(buf[0] == '<' & buf[buf.size() - 1] == '>')
                S.push_back(buf);
        }
        int sum = 0, now = 0;
        dfs(sum, now);
        for(int i = 0; i < res.size(); i ++ ) cout << res[i] << endl;
    }
    return 0;
}
~~~

#### Find the Fraction

<strong>[by Lambyy]</strong>这题基本上算是纯数学题吧, 且在ACM数论中针对分数领域题目出的少之又少, 所以此题算是冷门题.

题目是对n阶Farey Sequence中的第k项, 进行分母不大于m的分数逼近. 

所以第一步需要求待逼近分数. 

对于求Farey Sequence中项有朴素算法, 复杂度是O(n^2)的. 所以对于此题n 10^5的数量级是行不通的. 

Farey Sequence性质: 
<ul>
<li><strong>性质1</strong>&nbsp;&nbsp;如果a/b,x/y是F<sub>n</sub>中的相邻两项, 那么ay + 1 = bx.<br />
证明: 此结论可根据Fn的构造过程得出. </li>
<li><strong>推论1</strong>&nbsp;&nbsp;F<sub>n</sub>中任意相邻两项之差大于等于1/n(n-1).<br />
证明: 假设这两项顺次分别为a/b和p/q, 则
故得结论。</li></ul>

根据推论1，假设f(i)(1&le;i&le;n<sup>2</sup>)为F<sub>k</sub>中不大于i/n<sup>2</sup>的项数。则f(i+1)-f(i)&le;1。我们只需要在这些值中二分，求出一个满足f(i)=k的i，然后再求出Fn中小于等于i/n<sup>2</sup>的最大分数。先用O(nloglogn)的时间作计算f(i)的预处理，由于每次计算f(i)的时间复杂度为O(n)，二分的次数为O(logn)，最后一次求最大分数时，只要枚举所有分母即可，所以本操作的时间复杂度为O(nlogn)。
得出待逼近分数之后(方便下文解释，设为a/b)，要进行分数逼近操作。

由FareySequence构造方式可知，第m阶Farey数列包含了分母不大于m的所有分数，所以最终所求即是在第m阶Farey数列中最接近a/b的两个数。Farey数列是有序的，我们知道a/b的准确值是出现在第b阶Farey数列中的，利用Farey数列的生成特点，可以从第b阶Farey数列中的a/b准确值反推出第m阶Farey数列中最逼近a/b的两个数，这里b不小于m。

接下来便是一个递归逼近的过程.

* 对于a/b, 生成在第b阶Farey数列中它的前一项和后一项, c/d和e/f. 
    这里根据性质1, 用扩展gcd算法求解.
* 如果d和f均不大于m，那么c/d和e/f就是答案。由于c/d和e/f是第b阶Farey数列中最逼近a/b的数，也同时存在于第m阶Farey序列中，而第m阶Farey序列不可能有比第b阶Farey序列更好的逼近，这便是递归过程的结束条件。
* 如果d和f均大于m，那么令a/b等于c/d和e/f分母较小的那个，跳到1，继续递归。
* 如果d，f中一个大于m，另一个不大于m，这是显然不大于n的是一个答案。不妨设d>m，而f&le;m。我们注意到e/f这一个分数在第m阶Farey数列中就已经存在，而在第d级Farey序列中它与c/d相邻，这里m<d<b，由于Farey数列的特点，c/d左边的那一项与e/f共同生成c/d，因此c/d左边的那一项值为(c-e)/(d-f)，如果d-f值仍然大于n，考虑到c/d生成之前(c-e)/(d-f)是与e/f相邻的，他左边的一项,(c-2*e)/(d-2*f)，依此类推，我们可以找到k使得(d-k*f)<n，这时(c-k*e)/(d-k*f) 便是另一个答案。

这样便可以得到满足题意要求的两个分数。

关于本题结论 以及更多关于Farey Sequence 的知识, 请参考论文<a href="http://wenku.baidu.com/view/40edb37a32d7375a41780c9.html">《一类分数问题的研究》</a>.

~~~cpp 
#include <cstdio>
#include <cstring>
#include <cmath>
const int N = 100010;
long long n, A[N], m;

long long gcd(long long a, long long b) {
    return b ? gcd(b, a % b) : a;
}

long long Rank (long long a) {
    long long q, t, ans = 0;
    for (q = 1; q <= n; ++q)    A[q] = q * a / n;
    for (q = 1, ans = 0; q <= n; ++q) {
        ans += A[q];
        for (t = q * 2; t <= n; t += q) A[t] -= A[q];
    }
    return ans;
}

long long bsearch(long long k) {
    long long t, lt = 0, rt = n, mid;
    while (lt < rt) {
        mid = (lt + rt) >> 1;
        t = Rank(mid);
        if (t == k) return mid;
        if (t < k)  lt = mid + 1;
        else rt = mid - 1;
    }
    if (Rank(lt) > k & Rank(lt - 1) < k)   return lt - 1;
    else return lt;
}

void search(long long term, long long s, long long p, long long q, long long t1, long long &t2) {
    long long a, b, c, d, e, f, k, t = 1, i;
    t = gcd(s, n), a = s / t, b = n / t;
    t = gcd(p, q), c = p / t, d = q / t;
    if (term == 0) {
        t1 = a, t2 = b;
        return;
    }
    for (i = 1; i < term; i++) {
        k = (long long)((n + b) / (double)d);
        e = k * c - a, f = k * d - b;
        a = c, b = d, c = e, d = f;
    }
    t1 = c, t2 = d;
    return;
}

long long ext_gcd(long long a, long long b, long long x, long long& y) {
    long long t, ret;
    if (!b) {
        x = 1, y = 0;
        return a;
    }
    ret = ext_gcd(b, a % b, x, y);
    t = x, x = y, y = t - a / b * y;
    return ret;
}

void find(long long a,long long b,long long L1,long long &L2,long long &R1,long long &R2) {
    long long x, y;
    ext_gcd(a, b, x, y);
    x = (x + b) % b;
    L2 = x, L1 = (L2 * a - 1) / b;
    R2 = (x * (b - 1)) % b, R1 = (R2 * a + 1) / b;
}

void solve(long long a,long long b,long long L1,long long &L2,long long &R1,long long &R2) {
    if (b <= m) {
        L1 = R1 = a;
        L2 = R2 = b;
        return;
    }
    find (a, b, L1, L2, R1, R2);
    if (R2 <= m & L2 <= m)  return;
    while (R2 > m & L2 > m) {
        if (R2 > L2) {
            a = L1, b = L2;
            find (a, b, L1, L2, R1, R2);
        } else {
            a = R1, b = R2;
            find (a, b, L1, L2, R1, R2);
        }
    }
    long long t1, t2;
    while (L2 > m) {
        a = L1, b = L2;
        find (a, b, L1, L2, t1, t2);
    }
    while (R2 > m) {
        a = R1, b = R2;
        find (a, b, t1, t2, R1, R2);
    }
}

int main() {
//    freopen("F.in", "r", stdin);
//    freopen("F.out", "w", stdout);
    long long i, k, a, p, q, po, t1, t2;
    long long t, Up1, Up2, Down1, Down2;
    double mi, tmp;
    while (scanf ("%lld %lld %lld", n, &k, &m) == 3) {
        a = bsearch(k), mi = 1.00, po = 0;
        for (q = 1; q <= n; q++) {
            p = ((a + 1) * q - 1) / n;
            if (p * n > q * a) {
                tmp = (double) (p) / (double) (q);
                if (tmp < mi)  mi = tmp, po = q;
            }
        }

        if (po != 0) q = po, p = ((a + 1) * q - 1) / n;
        else q = n, p = a + 1;

        search(k - Rank(a), a, p, q, t1, t2);
        t = gcd(t1, t2);
        t1 /= t, t2 /= t;

        solve(t1, t2, Down1, Down2, Up1, Up2);
        printf("%lld/%lld %lld/%lld\n", Down1, Down2, Up1, Up2);
    }
    return 0;
}
~~~

#### Zero Pair

<strong>[by Xnozero]</strong>将`a*b=rev(a)*rev(b)`转化为`a/rev(a)=rev(b)/b`,预处理出范围内的 rev(a)的值,将a/rev(a)的分子分母约分后存入MAP，再对b进行类似的处理，从MAP中找到对应的值，统计总数即可。

~~~cpp 
#include<iostream>
#include<map>
#include<cstdio>
#include<cstring>
using namespace std;
map<pair<int,int>,int> hash;

int ext(int a, int b, int x, int &y)
{
    int t1, t2;
    if (!b)
    {
        x = 1;
        y = 0;
        return a;
    }
    else
    {
        t1 = ext(b, a % b, x, y);
        t2 = x;
        x = y;
        y = t2 - (a / b) * y;
        return t1;
    }
}
int gcd(int a, int b)
{
    if (a < b) return gcd(b, a);
    if (b==0) return a;
    return gcd(b, a%b);
}
pair<int,int> work(int a,int b)
{
    return make_pair(a/gcd(a,b),b/gcd(a,b));
}
pair<int,int> temp;
int main()
{
    // freopen("in.txt","r",stdin);
    int a,b,p;
    int x,y;
    int i,j;
    int ans;
    while (scanf("%d %d %d",a,&b,&p)==3)
    {
        ans=0;
        hash.clear();

        for (i=1;i<=a;i++)
        {
            ext(i,p,x,y);
            x=((x%p)+p)%p;
            if(x==0)
                x=p;
            hash[work(i,x)]++;
        }
        for (i=1;i<=b;i++)
        {
            ext(i,p,x,y);
            x=((x%p)+p)%p;
            if(x==0)
                x=p;
            temp=work(x,i);
            if (hash.find(temp)!=hash.end())
            {
                ans+=hash[temp];
            }
        }
        printf("%d\n",ans);
    }
    return 0;
}
~~~

<div>_____________________________解题报告分割线_____________________________</div>

比赛现场的情况是这样的

<a href="http://blog.oneplus.info/wp-content/uploads/2011/05/rank2.jpg"><img src="http://blog.oneplus.info/wp-content/uploads/2011/05/rank2.jpg" alt="" title="rank2" width="500" class="aligncenter size-full wp-image-303" /></a>

比较惊艳的几处:

<ul>
<li>第二、第四是两位哈三中OI的同学，第二的同学好像是NOI银，全场唯一一个搞定了羊的G，真强！</li>
<li>rank 14的同学来自能源学院，寒假时自学过一点C语言，是我程序设计实践的学生，也很强</li>
<li>尤波学长、bin3学长依旧成绩靠前</li>
<li>羊那天说了一句，“后生可畏啊”</li>
<li>刷刷…不说什么了</li>
</ul>

就这样子吧。
