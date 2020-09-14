---
layout: post
title: 最短路径算法总结
date: 2020-09-14 14:57 +0800
hero: https://source.unsplash.com/random
overlay: red
link: https://github.com/LukeLee233/shortest_path_algorithms
---

<!--enable mathjax-->
<head>
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({
            tex2jax: {
            skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
            inlineMath: [['$','$']]
            }
        });
    </script>
</head>

# 1. 最短路径算法所基于的假设
<!–-break-–>

- 图中的边权值非负
- 图中存在权值为负的边，但不构成负环
- 图中存在权值为负的边，并且构成负环

针对不同的假设，算法的适用性也会不同

# 2. Floyd-Warshall算法

该算法基于动态规划的思想，其中定义状态函数$f[k][i][j]$,
表示从$i$到$j$在只能经过前$k$个点的约束下，最短的路径长度。

$$
f[k][i][j] = \min(f[k-1][i][j],\quad f[k-1][i][k]+f[k-1][k][j]) \tag{1} \label{1}
$$

\eqref{1}式表示要么不使用第$k$个点做中继节点，要么使用第$k$个节点做中继节点。

- 可以用来求解任意两个点之间的最短路径
- 无法处理负权环的情况
- 可以处理有负权边的情况
- 空间复杂度$O(n^2)$,时间复杂度$O(n^3)$

## 2.1 滚动数组优化

由\eqref{1}式可以看出第$k$层的状态只取决于第$k-1$层的状态，
为此可以考虑使用滚动数组的方式来优化空间复杂度

<div class="notice" markdown="1">
考虑在滚动更新过程中，$f[i][j]$完成更新后，对$f[m][n]$进行更新

$$
f[m][n] = \min(f[m][n],\quad f[m][k]+f[k][n])
$$

如果$\\{m=i,k=j\\}$或者$\\{n=j,k=i\\}$,这时更新完成后的$f[i][j]$会参与到
更新过程中。因为这时$j=k$或$i=k$，则$f[i][j]=f[i][j]+f[j][j]$或
$f[i][j]=f[i][i]+f[i][j]$,这时更新后的数值与更新前的数值比并没有变化，
所以并不会影响求解的过程。

</div>

## 2.2 路径信息的计算

定义$path[i][j]$表示从点$i$到$j$所经过的节点k，那么就可以用递归的方式求得
最短的路径信息

<div class="notice" markdown="1">
假设$path[i][j]=k$,那么从$i$到$j$的最短路径就可以用如下递归表达式表示

$$
i \rightarrow path[i][k] \rightarrow k \rightarrow path[k][j] \rightarrow j
$$

</div>

<br><br>
# 3. Dijkstra算法

基于贪心的思想，用于求解单源最短路径的问题，只能用于求解非负数边的情况