tags: #optimization 

Sometimes the optimization doesn't converge
Maybe there's a phase that is so short it has almost no impact on the objective
Optimizer doesn't like how darn flat that space is
Added a small term to the objective concerning that short phase

Linked to [[Advanced problem formulation]]

## Main message
Multiobjective optimization is somewhat of a misnomer -- you actually have to have predefined weightings for each of the objectives you care about, or implement them as constraints.

## Context for multiobjective optimization
Most optimization algorithms assume the objective function returns a scalar, thus they are capable of only single-objective optimization. Some other algorithms, including (TODO: add some examples) are able to perform multiobjective optimization in some way. Of course the hope is that you can optimize two or more objective values at once, but the reality is that often those objective functions are at odds with each other.

Let's view aerostructural wing design for an example. In a simple trade-off, if you extend the wingspan you get more lift and aerodynamic performance, but your structural masses and costs become greater to withstand the larger load. This trade-off means that you cannot maximize the aerodynamic performance *and* minimize the structural weight -- there must be some sort of a balancing act. In reality we care about the total performance of the airplane, more than any subdiscipline, so our objective function usually captures effects from multiple disciplines at once.

## Weighted sum method
- the simplest way to combine objectives
- can show a manim animation very easily
- the scaling of each of the values greatly affects the results; think about the units
- this leads naturally into Pareto fronts

## Pareto front
- made in economics
- allows us to easily compare different designs
- sometimes they're really sharp, sometimes they're not
- the best way to produce a Pareto front is not necessarily the weighted sum method

## Epsilon constraint method
- this is the preferred way of creating Pareto fronts
- you vary the constraint value and perform optimizations at each one of the points
- this produces a more robust curve
- you can easily control the spacing for the Pareto front, whereas you wouldn't know it a priori in the weighted sum method
- makes sense to run two optimizations first; one with the first objective only and the other with the second objective only so you know the bounds for your epsilon constrained approach

