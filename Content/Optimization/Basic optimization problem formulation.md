tags: #optimization 
Objectives and constraints are functions of interest
Inequality vs equality constraints
Well defined and poorly defined problems (hand coded brachistochrone?)

GASPY and LEAPS teams:
often come to a decision
e.g. there's a feedback loop
Can either do it through direct connection or driving a constraint (tight vs loose coupling)
When to connect or constrain?
e.g. fuel weight is better as an equality constraint than a direct connection

It often seems in a lot of complicated mission cases that it's more helpful to do loose coupling
Requires a lot of trial and error

or other people, not just you
Eliot does okay (maybe check this)


## Main message
One of the most important steps in optimization is formulating well-posed and meaningful problems that you can interpret accurately. 

## The objective function
The objective is the measure that you are trying to minimize or maximize when performing optimization. Common objective functions include performance and cost metrics. You might be trying to minimize the cost of energy produced by a wind turbine or maximize the plant mass and revenue of a piece of farmland. Whatever your objective is, you need to quantify and model it in some way so the optimizer can find the optima.

Most representations of optimization problems seek to minimize the objective function so that the math is always the same. OpenMDAO assumes this as well, but if you want to maximize a value you can apply a `scaler` or `ref` using a negative value (such as -1), which will flip the minimization problem into a maximization problem.

An objective function is a type of a "function of interest." By definition, an objective function must return a single scalar value.

## Design variables
Design variables are any value that are being controlled by the optimizer. Design variables (DVs) often control the geometric, operational, or physical aspects of systems. Finding the optimal set of design variables for a given problem means that you have solved it. DVs can have any arbitrary shape and size, though optimization problems become more difficult to solve as the design space grows in dimensionality.

- you want to avoid linearly dependent DVs
- DVs can be discrete or continuous
- if possible, it's a good idea to minimize the number of DVs you start with
- if you have a large number of DVs, you should use gradient-based optimization as detailed in [[Why to use gradient-based optimizers]]


## Constraints
A constraint is another type of a "function of interest," alongside objective functions. A constraint is a way to limit the outputted values of a model by using an optimizer. Any value outputted by the model can be used as a constraint.

There are a few different categories of constraints.

Inequality constraints dictate that an outputted value from a model must be greater than or less than a desired constraint value. Equality constraints dictate that the outputted value must match the desired value to a certain tolerance.

-  include linear and nonlinear constraint delineation here?

