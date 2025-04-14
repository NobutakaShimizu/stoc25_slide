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

Given two $n \times n$ matrices $A$ and $B$, compute their product $C = AB$.

</div>

- $O(n^\omega)$-time algorithms for
  - $\omega = 2.373$ (Coppersmith-Winograd)
  
---
layout: top-title
color: amber-light
---

::title::

# Error-Correction

::content::

<div class="topic-box">

Suppose that we have a fast algorithm $M$ that computes $\epsilon$-fraction of the entries of $AB$ correctly.
Can we compute all entries of $AB$ correctly using $M$ as subroutine?

</div>

