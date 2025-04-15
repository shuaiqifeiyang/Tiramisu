---
title: "Numeric Methods"
date: 2022-01-24T12:03:15-08:00
draft: true
---

Solving linear systems

* small(up to 2000*2000)
  * is symmetric: modified Cholesky decomposition
  * LU decomposition (Blas, Lapack, Eigen)
* large
  * is sparse:
    * symmetric: sparse Cholesky / Conjugate Gradients (mesh is too crazy)
    * no symmetric: sparse LU
  * not sparse:  O(n^3)

Some library to solve linear systems: Pardiso, Taucs, Mumps

Intel 

* TBB: a library for parallel program
* MKL(Math Kernel Library)(Eigen is a wrapper of MKL)
* MMX/SSE/AVX



NEWTON-RAPHSON Methods

Time stepping ODE

* forward EULER's method
* backward Euler method



## Cholesky decomposition

**Hermitian matrix** (self-adjoint matrix): A complex square matrix that is equal to its own conjugate transpose

**Positive-definite matrix**: In mathematics, a symmetric matrix M with real entries is positive-definite if the real number $z^TMz$ is positive for every nonzero real column vector $z$.

A matrix $M$ is positive-definite if and only if it satisfies any of the following equivalent conditions.

- *M* is [congruent](https://en.wikipedia.org/wiki/Congruent_matrices) with a [diagonal matrix](https://en.wikipedia.org/wiki/Diagonal_matrix) with positive real entries.
  - In [mathematics](https://en.wikipedia.org/wiki/Mathematics), two [square matrices](https://en.wikipedia.org/wiki/Square_matrix) ***A*** and ***B*** over a [field](https://en.wikipedia.org/wiki/Field_(mathematics)) are called **congruent** if there exists an [invertible matrix](https://en.wikipedia.org/wiki/Invertible_matrix) ***P*** over the same field such that $P^TAP=B$
- *M* is symmetric or Hermitian, and all its [eigenvalues](https://en.wikipedia.org/wiki/Eigenvalue) are real and positive.
- *M* is symmetric or Hermitian, and all its leading [principal minors](https://en.wikipedia.org/wiki/Principal_minor) are positive.
- There exists an invertible matrix B with conjugate transpose $B^*$ such that $M=B^*B$

**Cholesky decomposition**: is a decomposition of a hermitian, positive-definite matrix into the product of a lower triangular matrix and its conjugate transpose 
