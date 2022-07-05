tags: #model_construction

## Main message
You need to use a nonlinear solver when there's backwards coupling or implicit systems; need to use linear solver when using derivatives for Newton solvers or optimizers.

## Context
- look, I get it, it's really confusing and I sometimes forget to put solvers on models
- but in 99% of cases you need a linear solver if you're using derivatives
- nonlinear solvers help solve the physical model, linear solvers help solve for the derivatives

## Some nonlinear solvers
- Newton
- NLBGS
- Broyden
- you can use these when you see feedback loops in your models

## Some linear solvers
- linear BGS
- direct solver
- PETScKrylov