---
layout: post
title: GSoC Week 2
tags: [gsoc, python, programming, maths]
comments: true
image:
 feature: gsoc.png
---

The 2nd week is now coming to an end, and by now I have a pretty good idea
about how things often don't work the way we want them to.

## So far

I trimmed down [PR 9262](https://github.com/sympy/sympy/pull/9262) to remove all
the parts not yet ready. It is undergoing review and should get merged soon.

Last week, I had planned to complete work on Laurent series by now, but it is still a work
in progress. Fortunately, while discussing it with my mentors, we realized that
handling Puiseux series is not as difficult as I had thought initially. 

Internally, all polynomials are stored in the form of a dictionary, with a tuple
of exponents being the key. So `x + x*y + x**2*y**3` is stored as
{(1, 0): 1, (1, 1): 1, (2, 3): 1}. For Puiseux series I need to be able to have
rational exponents as keys in the dict. This isn't an issue in Python 3 as it
evaluates `1/4` to `0.25` and the uses the decimal value as key. It doesn't work
in Python 2 as it evaluates `1/4` to `0` and hence all fractions less than 1
become 0. The solution to this is to use Sympy's Rational data type, which lets
us use the exact fraction as a key. This means that, hopefully, I will not need
to make any complex changes in the code of `ring`.

I still have a few days to go in this week, during which I will further explore
how to make the required changes.

There hasn't been much progress on the hashtable as both me and Sumith have been
busy with our PRs. Hopefully, we will look into it during the weekend.

## Next Week

* Make `ring_series` work with Puiseux series
* Write an interface to better handle the series, especially so that it
works with the rest of Sympy.

Cheers!
