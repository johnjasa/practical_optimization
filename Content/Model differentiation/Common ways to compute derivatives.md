tags: #differentiation 
FD, CS, by hand, AD

## Main message
There are many ways to compute partial derivatives: finite-differencing, complex-step, analytically by hand, or through algorithmic differentiation. The best method depends on your problem formulation, but the best implementation usually involves an intelligent mix of these methods.

## Finite differencing
- simplest and dumbest
- you simply perturb the function or model
- most prone to issues
- you don't have to think about it though
- if someone just hands you a black box you can do this
- coloring can somewhat help this but it's still very expensive, please don't do this

## Complex step
- really, CS is just FD but with complex numbers
- you can learn more about the theory from this book or paper
- the biggest practical consideration is that you need a complex-safe model
- OpenMDAO allows for this with typing, but some python, numpy, etc functions are not complex-safe

## Analytic by hand
- this is the most accurate and computationally efficient way to compute derivatives
- it's computationally very expensive
- there are many tips and tricks, some of which are
	- to remember and use calculus
	- to use wolfram alpha or similar
- it's quite developer time intensive to do this though, especially for large models
- for computationally expensive models or code that you will use a *lot* it makes sense to do analytic derivs

## Algorithmic differentiation
- this is where a computer does the differentiation for you; aka automatic differentiation
- can be done via source code transformation or operator overloading
- some packages exist to do this in Python, like tensorflow, Jax, etc
- Julia and other packages do this very well
- there are also tools like Tapenade
