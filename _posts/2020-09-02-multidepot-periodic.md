---
layout: post
title: HGA for Multidepot Periodic论文阅读
date: 2020-09-02 14:40 +0800
tags:
  - vrp
  - article
hero: https://source.unsplash.com/collection/190725/
link: https://pubsonline.informs.org/doi/abs/10.1287/opre.1120.1048
overlay: red
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


# 1. 问题定义
<!–-break-–>

## 1.1 CVRP

<div class="notice" markdown="1">
存在一个完全图$G=(\mathscr{V},\mathscr{A})$,其中$|\mathscr{V}|=n+1,
\mathscr{V}=\mathscr{V}^{DEP} \cup \mathscr{V}^{CST}$,$v_{0} \in
\mathscr{V}^{DEP}$表示仓库点，$v_{1...n} \in \mathscr{V}^{CST}$表示待服务点，
每一个服务有$2$个特征
1. 需求$q_{i} \geqslant 0$
2. 服务时长$\tau_{i} \geqslant 0$

$a_{ij} \in \mathscr{A}, (i,j) \in \mathscr{V}$表示从点$i$到点$j$的行驶距离，
$c_{ij} \geqslant 0$。每辆载具从仓库点出发，服务若干客户返回仓库，同时要保证
服务时间与载重约束，同时要最小化服务成本。
</div>

## 1.2 MDVRP

<div class="notice" markdown="1">
在CVRP的基础上，增加仓库点的数量，并且每个仓库点有$m_{i}$辆载具，
客户可以通过任意仓库点进行服务。
</div>

## 1.3 PVRP

<div class="notice" markdown="1">
在CVRP的基础上，增加时间维度$t$，每个客户{i}需要在时间周期$t$内被服务$f_{i}$次，
$L_i$表示对于客户$i$在$t$内所有的可能的服务方式。
问题的目标就是为每一个客户选择一个服务方式$pattern \in L_i$，
并基于该模式设计每个时期的相应服务路线。
</div>

## 1.4 MDPVRP

<div class="notice" markdown="1">
在MDVRP和PVRP的基础上进行融合，这时的目标变为为每个用户选择一个仓库点与服务模式
在选定服务仓库后，整个服务期间用户的的服务仓库不会发生改变。
</div>


# 2. 问题建模与对偶问题转化

## 2.1 决策变量

为了定义MDPVRP问题，引入两个0-1决策变量矩阵$y_{ipo}$与$x_{ijklo}$

- $y_{ipo}$表示第$i$个客户是否选择第$p$个服务方式与第$o$个仓库点，这个决策变量用于
  客户的服务方式进行建模，可以看做第一阶段决策。

- $x_{ijklo}$表示在第$l$天,从第$o$个仓库出发的的第$k$辆载具(一个载具对应一条路径)，
  所构成的服务路径中是否存在{i,j}边，这个决策变量用于对在第一阶段决策顺序确定的情况下，
  对客户的服务顺序进行建模。可以看做第二阶段决策。


<div class="notice" markdown="1">
此外引入常量0-1矩阵$a_{pl}$,表示第$l$天是否会在模式$p$中进行服务
</div>

## 2.2 目标函数

$$
\min \sum_{v_{i} \in V} \sum_{v_{i} \in V} \sum_{k=1}^{m} \sum_{l=1}^{t} \sum_{v_{o} \in V^{DEP}}c_{ij} \ast x_{ijklo}
$$

对所有的行驶成本求和并求最小值

## 2.3 约束条件

$$
\sum_{p \in L_{i}} \sum_{v_o \in V^{DEP}}y_{ipo}=1 ,\qquad v_{i} \in V^{CST} \tag{1} \label{1}
$$

\eqref{1}表示每个客户只能选择一种服务方式，服务方式包括仓库$o$的选择以及服务pattern  $p$的选择。

$$
\sum_{v_j \in V} \sum_{k=1}^{m}x_{ijklo} - \sum_{p \in L_{i}}a_{pl}\ast y_{ipo}=0 ,\qquad v_{i} \in V^{CST}; v_{o} \in V^{DEP};l=1...t \tag{2} \label{2}
$$

比较容易看出，在\eqref{2}中$\sum_{p \in L_{i}}a_{pl}\ast y_{ipo}$取值只能为$\\{0,1\\}$，该约束表明如果客户$i$选择
第$p$种服务方式以及第$o$个仓库，那么在第$l$天,如果该天属于该服务模式，则客户$i$
一定会存在于该天仓库$o$的服务路径上。

<div class="notice" markdown="1">
客户$i$被服务等价于至少有一条边$(i,j), j \neq i$存在
</div>

$$
\sum_{v_j \in V}x_{ojklo} \leqslant 1 ,\qquad v_o \in V^{DEP};k=1..m;l=1...t \tag{3} \label{3}
$$

\eqref{3}式表示对于每一天的每一个仓库的每一条路径，从仓库点最多有一个出口，
换句话说就是每辆载具最多只能使用一次

$$
\sum_{v_j \in V}x_{ijklo}=0 ,\qquad v_i,v_o \in V^{DEP}; k=1...m;l=1...t \tag{4} \label{4}
$$

\eqref{4}式表示选择从仓库点$o$出发，则该路径不能从其他仓库出发

$$
\sum_{v_j \in V}x_{jiklo} - \sum_{v_j \in V}x_{ijklo} = 0 ,\qquad v_i \in V;v_o \in V^{DEP};k=1...m;l=1...t \tag{5} \label{5}
$$

\eqref{5}式表示每一个点的出度和入度相同，即要需要保证构成回路

$$
\begin{eqnarray*}
\sum_{v_i \in V} \sum_{v_j \in V}q_i \ast x_{ijklo} &\leqslant& Q ,\qquad v_o \in V^{DEP};k=1...m;l=1...t \tag{6} \label{6}
\\
\sum_{v_i \in V} \sum_{v_j \in V}(c_{ij}+\tau_i) &\leqslant& T ,\qquad v_o \in V^{DEP};k=1...m;l=1...t \tag{7} \label{7}
\end{eqnarray*}
$$

\eqref{6},\eqref{7}式分别为载重约束以及最大行驶时间约束

$$
\sum_{v_i \in S} \sum_{v_j \in S}x_{ijklo} \leqslant \left | S \right | - 1 ,\qquad S \in V^{CST};\left | S \right | \geqslant 2;v_o \in V^{DEP};k=1...m;l=1...t \tag{8} \label{8}
$$

\eqref{8}式表示任意的客户之间不存在环路，只有仓库点参与后够成的环路


## 2.4 对偶问题的构建

### 2.4.1 MDVRP$\Rightarrow$PVRP问题

- 每一个仓库对应一个时间戳,
- 每一个客户在整个时间周期内的服务次数为$f_i=1$
- 抽象出一个虚拟仓库，原问题中距离矩阵$c_{ij}$变为$c_{ijl}$,
  即每个时刻的距离矩阵依赖于虚拟仓库的位置

### 2.4.2 MDPVRP$\Rightarrow$PVRP

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);"
    src="2020-09-02-MDPVRP/MDPVRP_dual.png">
    <div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999999;
    padding: 2px;">MDPVRP对偶问题</div>
</center>

<div class="notice" markdown="1">
这里$p_{jk}^{i} \in \\{1,...t\\}$
</div>

<br><br>
通过上述问题的转化，三类问题均可以看做PVRP问题进行统一求解
<br><br>

# 3 算法设计

## 3.1 算法框架

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);"
    src="2020-09-02-MDPVRP/HGSADC.png">
    <div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999999;
    padding: 2px;">Hybrid Genetic Search with Adaptive Diversity Control</div>
</center>


*[CVRP]: Capacitated Vehicle Routing Problem
*[MDVRP]: Multidepot Vehicle Routing Problem
*[PVRP]: Periodic Vehicle Routing Problem
*[MDPVRP]: Multidepot Periodic Vehicle Routing Problem
