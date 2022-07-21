tags: #model_construction #optimization 

# Main message
You must use a solver tolerance for convergence in line with your expectations and use case for the model. Specifically, your solver tolerance **must** be tighter (smaller number) than your optimization tolerance.

## What is solver tolerance?
- it's the criteria for when to stop solving a model, when the residuals are driven below the tol the solver is done
- R(x) < tol
- if you "tighten" a tolerance, you make it smaller, thus the solver must work harder
- if you "loosen" a tolerance, the solver has to converge the model less

## How to choose solver tolerance
- how much do you care about the actual answer?
- if you're not doing optimization, it's probably fine to use a looser tolerance
- especially if you're debugging your model it's okay to use a looser one
- for optimization you must use a solver tolerance that's the opt_tol^2, technically
- however, you can probably get away with a few orders of magnitude more than the opt tol, realistically. the actual value varies based on the model, solver, and optimizer you're using

## Examples where the solver tolerance is the issue
- when you compare vs CS and you find the comparison varies with solver tolerance
- if you tighten the tolerance and the issue is resolved then it might be that
- another case is when optimization moves into a space and jives around there for a while. however, this could be caused by a million different things unfortunately

