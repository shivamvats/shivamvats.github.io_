---
layout: post
title: GSoC Week 6
tags: [gsoc, python, programming, maths]
comments: true
image:
 feature: gsoc.png
tags: GSoC, SymPy
---

I successfully passed my mid term evaluation this week and now the second half
of my project has begun! It has been a challenging journey so far that has made
me explore new algorithms (some very ingenious) and read a lot of code (much
more difficult than I had imagined). This week, Mario whose code I am
working on, helped in a big way by showing how and where to improve the
algorithms. It is clear now that all the functions need to guarantee the order
of the series they output. We were planning to keep it optional but since
`ring_series` functions each other, an error in the order will propagate and
eventually make it unpredictable.

### So Far

[PR 9575](https://github.com/sympy/sympy/pull/9575) is ready for merge except
for a bug in `sympify` that converts `PythonRational` into float. 

I had a discussion with Mario on [PR
9495](https://github.com/sympy/sympy/pull/9495). He has suggested a lot of
improvements while dealing with fractional exponents, especially the fact that
Newton method may not be ideal in these cases. It is very interesting to try and
compare different algorithms and come up with ways to optimise them for out
needs. The scope for improvement is immense and we'll need to decide the order
in which we'll push the optimisations.

I started writing the `RingSeries` class for series evaluation in [PR
9614](https://github.com/sympy/sympy/pull/9614). I was supposed to update my
blog yesterday, but I dozed off while working on it. According to my current
approach, I am writing classes for all the functions so that they can be
represented symbolically. Another issue that needs to be tackled is expansion of
nested functions, things like `sin(cos(sin(x))`. This will need some work as
there are many approaches to tackle it. Currently, I evaluate the inner
functions( it they exist) recursively with `prec + 1`. This will work in simple
cases, but not if there are cancellations, eg, `sin(cos(x)) - sin(cos(x**2))`.

### Next Week

* Get [PR 9575](https://github.com/sympy/sympy/pull/9575) merged.

* Improve [PR 9495](https://github.com/sympy/sympy/pull/9495) and get it merged.

* Finalise the series class hierarchy and the `series` evaluation function.

The next phase of my project is in Symengine and there have been a lot of
improvements and changes there. I will need to play with the new stuff and
perhaps also think of ways to port `ring_series` there.

Cheers!
