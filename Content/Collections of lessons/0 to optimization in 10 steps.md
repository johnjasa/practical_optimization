tags: #lesson


This guide serves as a medium-length approach to developing an understanding of how to perform multidisciplinary design optimization (MDO) assuming no prior knowledge of MDO.
We assume that you have college-level training in engineering concepts, including differential equations, Python programming, and basic numerical methods.
Additionally, most all of the examples use OpenMDAO, so having experience with it or going through the documentation is beneficial.

Also, step 10 could arguably come first as it might inform how you set up the filesystem for these models and optimizations.


1) Building uncoupled feed forward models
	1) [[Using groups to organize models]]
	2) [[Connecting things vs promoting them]]
	3) [[Using N2]]
2) Problem formulation
	1) [[Basic optimization problem formulation]]
	2) [[Multiobjective optimization]]
	3) Optional: [[Slack variables vs equality constraints]]
	4) Optional: [[How to deal with discrete variables]]
3) Simple gradient-free opt
	1) [[When to use gradient-free optimizers]]
	2) [[Types of gradient-free optimizers]]
4) Get partial derivatives
	1) [[Common ways to compute derivatives]]
5) Gradient-based opt
	1) [[Why to use gradient-based optimizers]]
	2) [[Types of gradient-based optimizers]]
6) Building coupled models
	1) [[Implicit vs explicit]]
	2) [[Fixed point iterators vs Newton]]
7) Gradient-free multidisciplinary optimization
8) Total derivatives for coupled models
	1) [[Nonlinear vs linear solvers]]
	2) [[Total vs partial derivatives]]
9) Gradient-based multidisciplinary optimization
10) Coding standards and best practices
	1) [[Git]]
	2) [[Folder and package structure]]
	3) [[Tests]]
	4) [[CI]]