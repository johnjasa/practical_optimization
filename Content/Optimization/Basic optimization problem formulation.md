tags: #optimization 

Progress:
- [x] info outlined
- [x] info fleshed out
- [x] visuals developed
- [x] lecture recorded
- [x] video produced
- [x] video uploaded
- [ ] 1st round feedback received
- [ ] video refined based on feedback
- [ ] video reuploaded
- [ ] notebook finished


## Main message
One of the most important steps in optimization is formulating well-posed and meaningful problems that you can interpret accurately. 

## The objective function
The objective is the measure that you are trying to minimize or maximize when performing optimization. Common objective functions include performance and cost metrics. You might be trying to minimize the cost of energy produced by a wind turbine or maximize the bushels of corn produced and revenue of a piece of farmland. Whatever your objective is, you need to quantify and model it in some way so the optimizer can find the optima.

In general, you need your objective function to output a singular scalar value, though you can also perform [[Multiobjective optimization]]. If you're using gradient-based optimizers, your objective function should be smooth and differentiable.

Most representations of optimization problems seek to minimize the objective function so that the math is always the same. OpenMDAO assumes this as well, but if you want to maximize a value you can apply a `scaler` or `ref` using a negative value (such as -1), which will flip the minimization problem into a maximization problem.

An objective function is a type of a "function of interest," along with constraints.

## Design variables
Design variables are any value that are being controlled by the optimizer. Design variables (DVs) often control the geometric, operational, or physical aspects of systems. Finding the optimal set of design variables for a given problem means that you have solved it. DVs can have any arbitrary shape and size, though optimization problems become more difficult to solve as the design space grows in dimensionality.

In the most general sense, DVs can be "continuous" where they can take any number of infinite values between bounds, or "discrete" where only certain values or types are allowed. Examples of continuous design variables include any floating point number or value, such as thickness of a structural member, capacity of batteries, or twist of an airplane wing section. Discrete variables include the number of blades on a wind turbine, the number of passengers on a flight, or number of motors on a wing.

When solving a new optimization problem, you should use the smallest number of DVs you can and still have an interesting problem. You might want to throw the whole kitchen sink at the optimizer where you have all the DVs that you'd eventually want optimized, but that approach often results in optimizer non-convergence or non-sensical answers. It often pays to walk before you run and slowly build up the complexity of the optimization problems, solving each more complex problem consecutively.

When choosing what should be a design variable, you should avoid linearly dependent variables. What we mean by that is that if you have multiple DVs that essentially control the same physical system, you should remove some of those DVs. For example, if you are modeling an aircraft wing and have angle of attack (AoA) *and* twist all the way across the wing, there are infinite combinations of AoA and twist that result in numerically the same condition. Here, you would constrain the root twist of the wing to avoid this unnecessary complication in the design space.

If you're solving a problem with a large number of DVs, you should use gradient-based optimization as detailed in [[Why to use gradient-based optimizers]]. Gradient-based optimizers scale much better with number of design variables, and if your analysis cost is non-trivial, this quickly becomes the only viable way to perform optimization.


## Constraints
A constraint is another type of a "function of interest," alongside objective functions. A constraint is a way to limit the outputted values of a model by using an optimizer. Any value outputted by the model can be used as a constraint.

There are a few different categories of constraints.

Inequality constraints dictate that an outputted value from a model must be greater than or less than a desired constraint value. Equality constraints dictate that the outputted value must match the desired value to a certain tolerance.

When all constraints are satisfied, the corresponding design is said to be "feasible". If any constraint is not satisfied, the design is "infeasible". At the a given design point, if a constraint value is right on its bound (either upper or lower bound), it is said to be an "active" constraint. Otherwise, if the constraint has more wiggle room at a design point, it is an "inactive" constraint.

While solving an optimization problem, the optimizer can violate prescribed constraints. This is normal and gives the optimizer more freedom to move through the design space. For example, there might be multiple feasible regions within the design space and only by temporarily violating a constraint can the optimizer move between them. Hopefully, if the optimization converges successfully, all constraints are satisfied at the optimal design.

## Basic tips for formulating optimization problems
If we could write out all the tips you need to create and solve complex optimization problems, that'd be fantastic. Unfortunately, there are so many details and intricacies -- this entire course is basically about this topic. However, we can discuss the extreme basics here and get you started solving relevant problems for your models.

First of all, the guidance in this section assumes you already have a working model, have verified it and its gradients, and somewhat understand the design space. None of those items are trivial by themselves, but all of them are necessary to perform gradient-based optimization.

To reiterate, you want to start with the simplest optimization problem that is reasonable for you to solve. If you're doing an aircraft mission optimization, start with a steady-state cruise profile. If you want to find the optimal aircraft wing structure, start with a 1g flight condition in steady flight and control just a few design variables. You want to simplify both the optimization problem and the complexity of the analyses to minimize potential sources of trouble.

Then, run a few iterations of the optimization algorithm to see what happens. Make sure the optimizer is taking reasonable steps and progressing through the design space. If the model analysis fails, examine what caused the failure and create a failsafe condition accordingly. Optimizers often push models beyond what designers might think is reasonable. If your model has some small bug or inconsistency, optimizers do a great job of finding those.

After you've run a few iterations of the optimization problem, refine the problem if need be and now run an optimization to convergence. You can then postprocess the results and see if it matches your intuition. if it doesn't, determine the physical reasoning behind the results and see if you should add or remove constraints, design variables, or change the objective function.

Next you need to iterate on the problem formulation and continue solving more complex problems. Only by interpreting and reformulating optimization problems and results can you get to meaningful answers. A push-button solution for optimization is not possible -- it requires people like you, the practitioner, to use your expertise to interpret the results.

We will cover many more tips in the [[Advanced problem formulation]] section, including deciding when to add a constraint vs. having the analysis solve for the value, how to determine the correct parameterization for a design space, and what makes poorly and well-defined optimization problems.