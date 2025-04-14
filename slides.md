---
theme: neversink
layout: cover
title: Error-Correction of Matrix Multiplication Algorithms
info: |
  ## Error-Correction of Matrix Multiplication Algorithms
  STOC2025

author: Nobutaka Shimizu
mdc: true
css: unocss
style: |
  @import './styles/custom.css';

fonts:
  sans: 'Roboto'
  mono: 'Fira Code'
  weights: '400,500,700'
  italic: true
favicon: 'https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@6/svgs/solid/book.svg'
themeConfig:
  primary: '#1976d2'


---

# Error-Correction of Matrix Multiplication Algorithms

Shuichi Hirahara (National Institute of Informatics)

[Nobutaka Shimizu](https://sites.google.com/view/nobutaka-shimizu/home) (Institute of Science Tokyo)

<div style="position: absolute; bottom: 20px; font-size: 0.8em; width: 100%; text-align: center;">
June 24th @STOC2025
</div>



---
layout: top-title
color: amber-light
---

::title::

# Matrix Multiplication

::content::

<div class="topic-box">

Given two matrices $A, B \in \Fp^{n\times n}$, compute their product $AB$.

</div>

- $O(n^\omega)$-time algorithms for
  - $\omega = 2.373$ (Coppersmith-Winograd)
<!-- TODO: history of matrix multiplication-->
  
---
layout: top-title
color: amber-light
---

::title::

# Problem Setting

::content::

<div class="question">

Given a fast algorithm $M$ that computes **$\alpha$-fraction** of the entries of $AB$ correctly for **random** input $A,B \sim \Fp^{n\times n}$,
can we compute **all** entries of $AB$ correctly for **arbitrary** $A,B\in\Fp^{n\times n}$?

</div>

- Introduced by <a class="cite-reference" href="https://drops.dagstuhl.de/entities/document/10.4230/LIPIcs.APPROX/RANDOM.2024.34">\[Gola, Shinkar, Singh, RANDOM'24\]</a>
- Worst-case-to-average-case reductions
  - <a href="https://www.sciencedirect.com/science/article/pii/002200009390044W?via%3Dihub" class="cite-reference">\[Blum, Luby, Rubinfeld, JCSS'93\]</a>
  - <a href="https://dl.acm.org/doi/10.1145/3519935.3520041" class="cite-reference">\[Asadi, Golovnev, Gur, Shinkar, STOC'22\]</a>
  - <a href="https://dl.acm.org/doi/10.1145/3564246.3585189" class="cite-reference">\[Hirahara, Shimizu, STOC'23\]</a>
  - In these works, average-case solvers are supposed to compute **all** entries of $AB$ for random $A,B\sim\Fp^{n\times n}$


---
layout: top-title
color: amber-light
---

::title::

# Motivation

::content::

- Theoretically fast algorithms are not practical due to heavy constant factors.
- Emerge of fast algorithms utilizing **physical system**

---
layout: top-title
color: amber-light
---

::title::

# Problem Setting (Formal)

::content::

<div class="definition">

The **agreement** of two matrices $A,B\in\Fp^{n\times n}$ is defined as

$$
  \begin{align*}
    \agr(A,B) &:= \Pr_{i,j\sim[n]}[A(i,j) = B(i,j)]
  \end{align*}
$$

</div>

We start with an algorithm $M$ such that

$$
  \begin{align*}
    \Exp_{\substack{A,B\sim\Fp^{n\times n} \\ M}}[\agr(M(A,B),AB)] &\ge \alpha
  \end{align*}
$$
- Expectation is taken over the random instance $A,B\sim\Fp^{n\times n}$ and the internal randomness of $M$

<div class="topic-box">

Our goal: worst-case solver with almost the same running time as $M$

</div>

---
layout: top-title
color: amber-light
---

::title::

# Our Result: Large Field

::content::

<div class="theorem">

Suppose $p > 10/\alpha$.
If there exists an algorithm $M$ that runs in time $T(n)$ and and satisfies
$$
  \begin{align*}
    \Exp_{\substack{A,B\sim\Fp^{n\times n} \\ M}}[\agr(M(A,B),AB)] &\ge \alpha,
  \end{align*}
$$

then there exists a $T(n)\cdot\polylog(n)\cdot \poly(1/\alpha)$-time algorithm $M'$ that satisfies

$$
  \begin{align*}
    {}^{\forall}A,B\in\Fp^{n\times n}, \quad \Pr_{M'}[M'(A,B)=AB] \ge \frac{2}{3}.
  \end{align*}
$$

</div>


---
layout: top-title
color: amber-light
---

::title::

# Our Result: Small Field

::content::

<div class="theorem">

If there exists an algorithm $M$ that runs in time $T(n)$ and and satisfies
$$
  \begin{align*}
    \Exp_{\substack{A,B\sim\Fp^{n\times n} \\ M}}[\agr(M(A,B),AB)] &\ge \frac{2}{p}+\varepsilon,
  \end{align*}
$$

then there exists a $T(n)\cdot\polylog(n)\cdot \poly(1/\varepsilon)$-time algorithm $M'$ that satisfies

$$
  \begin{align*}
    {}^{\forall}A,B\in\Fp^{n\times n}, \quad \Pr_{M'}[M'(A,B)=AB] \ge \frac{2}{3}.
  \end{align*}
$$

</div>

- Outputting random matrices achieve $\frac{1}{p}$-agreement
- The above reduction has an optimal agreement up to factor two.