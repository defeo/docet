---
title: Introduction to SageMath
addons:
  slideshow: yes
  highlightjs: yes
  mathjax: yes
  style_goodies: yes
category: class
description: ECC summer school
tags: SageMath, elliptic curves
---

<section>

# Introduction to SageMath

by [Luca De Feo](http://defeo.lu/)

[ECC summer school](http://ecc2015.math.u-bordeaux1.fr/index.php?category=school)

September 23-25, 2015. Bordeaux.

</section>
<section>

## What is SageMath?

**SageMath** (formerly **Sage**) is a free open-source mathematics
software system licensed under the GPL.

- It builds on top of many existing open-source packages: NumPy,
  SciPy, matplotlib, Sympy, Maxima, Pari/GP, GAP, FLINT, R and many
  more.
- Accesses their combined power through a common Python-based
  language, or directly via interfaces or wrappers.

Official downloads, docs, etc.: <http://www.sagemath.org/>

**Mission statement**

> Creating a viable free open source alternative to Magma, Maple,
> Mathematica and Matlab.
{:.cite}

</section>
<section>

## Facts and numbers

- Started in 2004 by [William Stein](http://wstein.org/);
- Developed by researchers, students and engineers for researchers and
  students (and engineers?);
- A community of >500 developers
- A company [SageMath, Inc.](http://sagemath.com/), established in
  2015;
- 19K tickets in the
  [issue tracker](http://trac.sagemath.org/wiki/TicketReports), 39K
  [commits](https://github.com/sagemath/sage/), 1.8M LOCs (native
  code);
- ~70 community meetings
  ([Sage Days](http://wiki.sagemath.org/Workshops)) in 10 years.

</section>
<section>

## No, seriously, what is it?

- A distribution of mathematical software (NumPy, SciPy, matplotlib,
  Sympy, Maxima, GAP, FLINT, R,...),
- A common Python-based interface, including interfaces to proprietary
  software (Magma, Mathematica, ...),
- Native Python/Cython code implenting more functionality,
- Two *web-based notebook* interfaces developed in house + Jupyter
  integration,
- [SageMathCloud](http://cloud.sagemath.com/), a *spinoff* project
  hosting collaborative math projects (Jupyter, Sage, LaTeX, ...) in
  the cloud.

### SageMath's development model

- Open source, Community driven,
- Peer-reviewed contributions via issue tracker
  <http://trac.sagemath.org>.

**You can contribute too!**
{:.centered}
 
</section>
<section>

## Using SageMath

### On your own computer

- Download from <http://sagemath.org>

- install,

- Run one of these:

  ~~~
  sage
  sage --notebook
  sage --notebook ipython
  ~~~

### In the cloud

- Create an account on <https://cloud.sagemath.com>,
- Create a new project, then
  - Create a new terminal and type `sage`, or
  - Create a new *SageMath Worksheet*, or
  - Create a new *Jupyter Notebook*.

</section>
<section>
<style >
@keyframes caret {
0% { opacity: 1 }
50% { opacity: 0 }
100% { opacity: 1 }
}
#caret { animation: caret 1s step-start infinite }
</style>

## SageMath interfaces

### Batch execution

- Write `.sage` or `.py` files in your favorite editor,
- Link to SageMath library,
- Execute from the command line.

### REPL (Based on IPython)

<pre class="compact bash"><code>user@host:~$ sage
┌────────────────────────────────────────────────────────────────────┐
│ SageMath Version 6.8, Release Date: 2015-07-26                     │
│ Type "notebook()" for the browser-based notebook interface.        │
│ Type "help()" for help.                                            │
└────────────────────────────────────────────────────────────────────┘
sage: 1+1
2
sage: <span id="caret">_</span>

</code></pre>

</section>
<section>

## SageMath interfaces

### SageMath worksheet

- Web-based notebook format,
- If you know SageMath, you probably know this one,
- Not supported anymore, bound to disappear.

### SageMath worksheet (SageMathCloud)

- New notebook application for collaborative writing,
- Exclusive to SMC,
- Destiny uncertain.

### Jupyter notebook

- Spinoff project of IPython
- Notebook webapp for generic scientific computing,
- Supports
  [many different languages](https://github.com/ipython/ipython/wiki/IPython-kernels-for-other-languages):
  Python, Julia, R, Haskell, Sage, ...

</section>
<section>

## Using subsystems from SageMath

### In the REPL or SageMath worksheet

~~~
sage: %gp

  --> Switching to PARI/GP interpreter <--

pari: 1+1
2
pari: ffinit(13,2)
Mod(1, 13)*x^2 + Mod(1, 13)*x + Mod(12, 13)
~~~

### In Jupyter

Not sure... upcoming?

</section>
<section>

## Hands on!

### If you have SageMath on your laptop

Check your version, 6.8 is best

~~~
user@host:~$ sage --version
SageMath Version 6.8, Release Date: 2015-07-26
~~~
{:.bash}

launch

~~~
sage --notebook ipython
~~~
{:.no-highlight}

you might need to point your browser to <http://localhost:8080>.

### If you have a SageMathCloud account

Simply open a new Jupyter Notebook.

### [Go to the demo!]({% include nbviewer.url url='assets/jupyter/2015-09-23-sagemath-demo.ipynb' %})
{:.centered}

</section>
