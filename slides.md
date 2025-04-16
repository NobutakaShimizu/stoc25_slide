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
  - Average-case solvers are supposed to compute **all** entries of $AB$ for random $A,B\sim\Fp^{n\times n}$


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

<div class="topic-box">

Our goal: worst-case solver with almost the same running time as $M$

</div>

---
layout: top-title
color: amber-light
---

::title::

# Our Result (1/3): Large Field

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

- <a href="https://arxiv.org/abs/2305.13945" class="cite-reference">\[Gola, Shinkar, Singh, RANDOM'24\]</a> gave the same reduction for $\alpha > 7/8$
- If $\Fp$ is large enough, we can error-correct a large fraction (say, 99\%) of errors.
- Proof is based on ECC (Reed-Solomon code)

---
layout: top-title
color: amber-light
---

::title::

# Our Result (2/3): Small Field

::content::

<div class="theorem">

If there exists an algorithm $M$ that runs in time $T(n)$ and and satisfies
$$
  \begin{align*}
    \Exp_{\substack{A,B\sim\Fp^{n\times n} \\ M}}[\agr(M(A,B),AB)] &\ge \frac{2}{p}+\varepsilon,
  \end{align*}
$$

then there exists a $O_{p,\varepsilon}(T(n)\cdot\polylog(n))$-time algorithm $M'$ that satisfies

$$
  \begin{align*}
    {}^{\forall}A,B\in\Fp^{n\times n}, \quad \Pr_{M'}[M'(A,B)=AB] \ge \frac{2}{3}.
  \end{align*}
$$

</div>

- Hidden constant factor in $O_{p,\varepsilon}(\cdot)$ is quite large (roughly $p^{\poly(p,1/\varepsilon)}$)
- Agreement is optimal up to factor two (random matrix achieves $1/p$-agreement)

---
layout: top-title
color: amber-light
---

::title::

# Our Result (3/3): Nonuniform Reduction

::content::

<div class="theorem">

If there exists an algorithm $M$ that runs in time $T(n)$ and and satisfies

$$
  \begin{align*}
    \Exp_{\substack{A,B\sim\Fp^{n\times n} \\ M}}[\agr(M(A,B),AB)] &\ge \frac{1}{p}+\varepsilon,
  \end{align*}
$$

then, in time $O_{p,\varepsilon}(n^3)$, we can construct a size-$T(n)\cdot\poly(\log n,p,1/\varepsilon)$ circuit $M'$ that satisfies

$$
  \begin{align*}
    {}^{\forall}A,B\in\Fp^{n\times n}, \quad \Pr_{M'}[M'(A,B)=AB] &\ge \frac{2}{3}.
  \end{align*}
$$

</div>

- Reduction with poly-time preprocessing
- Optimal agreement at the cost of nonuniformity
- Proof is based on XOR Lemma (average-case complexity)

---
layout: top-title
color: amber-light
---

::title::

# Related work

::content::

- <a href="https://arxiv.org/abs/2305.13945" class="cite-reference">\[Gola, Shinkar, Singh, RANDOM'24\]</a> gave the same reduction for $\alpha > 7/8$
  - They also gave a reduction for $p=2$ and $\alpha=1/2+\varepsilon$ under the assumption that $M$ has **one-sided** error (it satisfies $M(A,B)_{i,j}=1$ whenever $(AB)_{i,j}=1$)
  - Our reduction: $M$ can have two-sided error but is need a preprocessing
- <a href="https://link.springer.com/article/10.1007/s00453-016-0202-3" class="cite-reference">\[Gąsieniec, Levcopoulos, Lingas, Pagh, Tokuyama, Algorithmica'17 \]</a> showed how to compute $AB$ given three matrices $A,B,C\in\Fp^{n\times n}$ such that $\agr(AB,C)\ge 1-1/n$.
  - $n$ entries can be wrong (our reduction allows, say, $0.99n^2$ errors)
  - Their setting is more restrictive than ours (we are allowed to query the product of random matrices for many times)

---
layout: top-title
color: amber-light
---

::title::

# Additional Remark

::content::

- We believe that our nonuniform reduction is **practical** if $\abs{\Fp}$ is small
  - running time overhead is $p\cdot \poly(1/\varepsilon) \cdot \log n$
  - simple and thus hidden constant factor is reasonably small
- Our uniform reductions are based on **efficiently encodable/list-decodable codes** with linear rate
  - specifically, we use Reed-Solomon codes and expander-based codes
  - If the code admit a practical list-decoding algorithm, then our reduction is also practical
- In our follow-up work (to appear in ICALP25), we obtained **uniform** reduction with **optimal** agreement $\alpha = 1/p + \varepsilon$
  
---
layout: section
color: amber-light
---

# Proof of Uniform Reduction

---
layout: top-title
color: amber-light
---

::title::

# Basic of Error-Correcting Codes

::content::

- An **encoding function** is a linear map $\Enc\colon \Fp^n \to \Fp^N$ for $N\ge n$
  - The image $C = \Enc(\Fp^k)$ is called a **code** and $x\in C$ is called a **codeword**
  - **distance** = $\min_{x,y\in C,x\ne y} \dist(x,y)$
    - $\dist(\cdot,\cdot)$ is the normalized Hamming distance
- For $x\in \Fp^N$ and $\rho\in[0,1]$, let $\ball(x,\rho)=\{ y\in\Fp^N \colon \dist(x,y)\le\rho \}$

<div class="topic-box">

  **list-decoding.**
  Given $x\in\Fp^N$, output $C\cap \ball(x,\rho)$.

</div>

- $\#$ of codewords in $\ball(x,\rho)$?
- fast algorithm?