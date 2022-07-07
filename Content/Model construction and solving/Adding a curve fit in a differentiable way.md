tags: #model_construction #optimization #differentiation 


## Main takeaway
If you're fitting a curve or surface to data and want to ever use gradient-based optimizers, make sure to do it in a differentiable way.

## Intro and motivation
There are times that we want to fit a curve to data.
This data can be 1-dimensional or n-dimensional and may be regularly spaced, irregularly spaced, or sparse.
These fits go by many names, including regressions, surrogate models, metamodels, splines, and response surfaces.
This topic is inherently related to all three broad categories in the course.

This problem naturally crops up in many different places, such as:
- Engine performance data (reach out to [[Justin]] for example from MIT guy)
- Aerodynamic lift data
- Geospatial resource mapping (gold, soil, weather, etc)

For simplicity, we will use 1-dimensional examples here.

## Simple approach
A straightforward approach is a piecewise linear approximation of the data set.
However, this produces C1 discontinuities at the data points, which means that the derivative changes instantly and thus is not well-defined.
This potentially causes a problem for gradient-based optimizers who rely on accurate and smooth gradient information.

Imagine when the optimal point is near one of those discontinuous points.
The optimizer would struggle to correctly iterate there and may be ill-behaved.

## How to add a smooth and differentiable curve fit
Instead of using a piecewise linear fit, we could use a piecewise cubic spline, or many other forms of nonlinear surrogate modeling techniques.
Take our example from before and fit a piecewise cubic spline to it.
Now the resulting interpolation is smooth, continuous, and well-suited for gradient-based optimizers.

There are many packages to help you do this, including Scipy, SMT, and OpenMDAO.
OpenMDAO has built-in components to help you do this, including `SplineComp` and `MetaModels`.
These all compute the derivatives automatically by using the built-in functionality provided by OpenMDAO.

All this being said, getting a reasonable and accurate fit for your data is important.
Always verify the correctness of your curve fits by performing leave-one-out and other testing.
[[Creating high-quality surrogate models]] has much more information about this.