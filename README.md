# Everything you need to know about ChainRules 1.0

talk at JuliaCon 2021: https://www.youtube.com/watch?v=a8ol-1l84gc

## Abstract
ChainRules is an automatic differentiation (AD)-independent ecosystem for forward-, reverse-, and mixed-mode primitives.
It comprises ChainRules.jl, a collection of primitives for Julia Base, ChainRulesCore.jl, the utilities for defining custom primitives, and ChainRulesTestUtils.jl, the utilities to test primitives using finite differences.
This talk provides brief updates on the ecosystem since last year and focuses on when and how to write and test custom primitives.

## Description
Automatic differentiation (AD), the ability to efficiently evaluate derivatives of arbitrary functions without computing derivatives by hand, enables efficient learning of many mathematical models.
There are two components to every AD system: a collection of primitives (also called sensitivities or adjoints), and a way to keep track of and combine primitives using the chain rule of calculus in order to compute derivatives of arbitrary functions.
While AD systems differ greatly in the latter, the set of primitives can be shared among them.

The ChainRules ecosystem provides the AD-independent collection of primitives for Julia Base (ChainRules.jl), utilities for defining custom primitives (ChainRulesCore.jl), and utilities for testing custom primitives using finite differences (ChainRulesTestUtils.jl).
While not needed in principle, the ability to define custom primitives provides a way to speed up the computation by applying domain knowledge or mathematical insight, or get around limitations and performance issues of individual AD systems.
In addition, ChainRulesCore.jl provides a suite of expressive differential types which allow comparing derivatives across multiple AD systems.

Since last year the ecosystem has matured considerably, improving the user experience in a number of ways. Improvements include:

- It is now possible to write rules for higher order functions (e.g. map) by calling back into the AD system.
- `@non_differentiable` makes it easy to define rules for non-differentiable functions
- Testing custom primitives became easier since a random tangent (usually) does not have to be provided
- It is now possible to test `f/rrule`-like functions, meaning AD systems can be tested
- ChainRules is now used by Zygote, Diffractor, Yota, Nabla, and ForwardDiff2.

This talk will start by briefly introducing the ChainRules ecosystem, and highlighting the most important new features since last year.
Those unfamiliar with the general idea of ChainRules are encouraged to watch last year’s talk on ChainRules first, since the core of the talk is a comprehensive guide to using, writing, and testing custom primitives.
In particular, the talk will explain when it is advantageous to write custom primitives compared to using an AD system on its own, the interface for writing custom primitives and the associated supporting functionality, as well as why and how to test primitives by finite differencing methods.
