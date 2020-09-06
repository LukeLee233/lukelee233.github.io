---
layout: post
title: 文章参数说明
date: 2020-09-05 15:29 +0800
tags:
  - vrp
hero: https://source.unsplash.com/collection/190725/
overlay: purple
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

#  1 算法类别
<!–-break-–>

## 1.1 全局参数

| 参数名       | 说明                                     | 默认值 |
|:-------------|:-----------------------------------------|:-------|
| phase number | 搜索执行次数，一次执行表示一次完整的搜索 | 1      |
| random seed  | 随机数种子                               | 0      |


## 1.2 邻域搜索

| 参数名                  | 说明                                                                                         | 默认值 |
|:------------------------|:---------------------------------------------------------------------------------------------|:-------|
| neighbor search mode    | 邻域搜索模式 1. RTRIDP 2. IDPRTR 3. 随机                                                     | random |
| neighbor size           | 邻域表达小                                                                                   | 25     |
| significant search      | 在一次可行下降搜索中，如果实际move次数小于该阈值，则结束可行下降搜索                         | 5      |
| local ratio             | 在一次可行下降搜索中，如果没有导致成本变化的move占总move的比重超过该阈值，则结束可行下降搜索 | 0.8    |
| max RTR search cycle    | 随机禁忌下降搜索过程中，最大允许搜索次数，该参数的作用类似与number of children               | 50     |
| local minimum threshold | 在邻域搜索中，判断是否到达局部最优点                                                         | 40     |
| tabu step               | 在劣解可行搜索过程中，禁忌步数                                                               | 500    |
| infeasible distance     | 在非可行邻域搜索中，当前解距离可行区域的距离阈值，大于为过远，反之为过近                     | 0.3    |


## 1.3 种群搜索

| 参数名       | 说明                    | 默认值 |
|:-------------|:------------------------|:-------|
| evolve steps | 种群搜索总进化次数      | 5      |
| pool size    | 种群大小                | 5      |
| QNDF weights | 种群解中解质量-距离参数 | 0.6    |


<div class="notice" markdown="1">
在种群搜索中，解的fitness由如下计算:
$f(s)=QNDF \ast cost(s) + (1-QNDF) \ast mean(dist(s,{s}'))$
</div>