tags: #optimization 

- [x] main message created
- [ ] main message verified with someone
- [x] info outlined
- [x] info fleshed out
- [ ] visuals ideated
- [ ] visuals developed
- [ ] lecture recorded
- [ ] video produced
- [ ] video uploaded
- [ ] 1st round feedback received
- [ ] video refined based on feedback
- [ ] video reuploaded
- [ ] re-render and reupload

- [ ] notebook created
- [ ] notebook text completed
- [ ] notebook examples completed and checked

Visualizations:
- [ ] show the bits for a genetic algo from the mdobook
- [ ] show a particle swarm method converging
- [ ] show simplex method with the triangles

## Main message
There are many different types of gradient-free optimizers, including genetic algorithms, particle swarm methods, approximated simplex methods, and more. The best method to use varies based on your problem formulation and desired outcome.

## Context
The focus of this course is not to explain the theory of each one of these methods in detail. Instead, I'll briefly explain how the method works in practical terms, then comment on the types of problems or areas where this method works well.

## Genetic algorithms
Genetic algorithms (GAs), operate by constructing a bit-based representation of different designs and combining them in an evolutionary-esque manner. Imagine a "generation" of 50 designs which are evaluated and then the best designed are combined together in some prescribed manner to get the next generation of 50 designs. The idea originated from crossing "genes" which describe a design, much like actual organisms. GAs are well-suited for discrete (integer or mixed-integer) problems.

Although GAs make intuitive sense as they follow the same idea as real-world evolution, they are not particularly efficient at exploring the design space of highly dimensional problems. To be clear, they converge relatively slowly given the number of function evaluations needed. However, they are useful for exploring a design space in an exhaustive and stochastic manner.

## Particle swarm methods
Particle swarm optimization (PSO) methods iteratively solve problems by moving a swarm of designs ("particles") around the design space until convergence is reached. As these points move through the design space, they have some notion of velocity and momentum that govern how the designs vary iteration by iteration.

A real-world analogy is a swarm of mosquitos moving in space trying to find a meal. They each individually exist in a point and as a group in a swarm, have some velocities, and are on the hunt for the best meal.

PSOs are a metaheuristic and make few assumptions about the type of problem being solved. This is useful to explore the design space when you know nothing beforehand.

## Approximated simplex methods
[Powell's Derivative-Free Optimization](https://www.pdfo.net/docs.html#introduction) is an example of a class of methods that essentially follow the same steps as some gradient-based methods, especially sequential quadratic programs (SQPs), but do so without any gradient information. Basically, these methods construct simplexes using only function values to solve general nonlinear optimization problems.

The most well-known of these algorithms is COBYLA (constrained optimization by linear approximation). Without getting into the theory or math, you can think of COBYLA as a method akin to the gradient-based method SLSQP, but COBYLA is a bit more robust for noisy functions. This robustness comes at a computational cost. Again, because no derivative information is used, convergence is not competitive with gradient-based optimizers, especially for highly dimensional problems.
