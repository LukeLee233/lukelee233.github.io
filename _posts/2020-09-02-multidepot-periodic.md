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


# 问题定义
<!–-break-–>

# 1.1 CVRP

<div class="notice" markdown="1">
存在一个完全图$G=(\mathscr{V},\mathscr{A})$,其中$|\mathscr{V}|=n+1,
\mathscr{V}=\mathscr{V}^{DEP} \cup \mathscr{V}^{CST}$,$v_{0} \in
\mathscr{V}^{DEP}$表示仓库点，$v_{1...n} \in \mathscr{V}^{CST}$表示
</div>

*[CVRP]: Capacitated Vehicle Routing Problem
*[MDVRP]: Multidepot Vehicle Routing Problem
*[PVRP]: Periodic Vehicle Routing Problem
*[MDPVRP]: Multidepot Periodic Vehicle Routing Problem
