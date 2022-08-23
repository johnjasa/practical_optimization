tags: #model_construction 
related lessons:
[[Fixed point iterators vs Newton]]
[[Solving coupled systems]]
[[What solver tolerance should I use]]
[[What solver convergence looks like]]
[[How to debug solvers]]
[[Nonlinear and linear systems and solvers]]
[[Hierarchical linear solvers]]
[[Nested nonlinear solvers]]

- [x] main message created
- [ ] main message verified with someone
- [x] info outlined
- [x] info fleshed out
- [x] visuals ideated
- [x] visuals developed
- [x] lecture recorded
- [x] video produced
- [x] video uploaded
- [ ] 1st round feedback received
- [ ] video refined based on feedback
- [ ] video reuploaded
- [ ] re-render and reupload

- [x] notebook created
- [x] notebook text completed
- [x] notebook examples completed and checked

Viz ideas:
- [x] 3.6 from Martins and Ning
- [ ] an N2 where there's no backwards coupling but there is an implicit component to show when you need a Newton solver
- [x] show NLBGS aerostructural video when discussing fixed point iterators
- [x] show Newton solver video and link to it


## Main message
For nonlinear and linear systems there are various solvers that can converge your system. The best solver to use is highly problem dependent but the goal of this lecture is to be able to recognize a reasonable starting configuration for your systems.

## Brief introduction to solvers
The goal of this lesson isn't to introduce the math or theory behind solvers, but more to give a brief introduction to the different classes of solvers and when you would practically want to use one over the other. Throughout this lesson, I will reference other resources that go into much more detail about the solvers themselves and how they operate on systems.

**I highly recommend you read Section 3.6 from Martins and Ning's book *Engineering Design Optimization*** before proceeding with this lesson. That section concisely lays out the main differences between solver types. To start, I'm going to share Fig. 3.3 from the book. This figure shows the categories of solvers relevant for MDO. Some solver types, such as the fixed point iteration methods, are useful for solving both linear and nonlinear systems.

One main distinction between solver types I want to highlight is if they are *direct* or *iterative*. Direct solvers factorize the linear system in a single step to obtain the solution whereas iterative solvers iterate through state values until convergence. Direct solvers are only available for linear systems. For small problems, direct linear solvers make the most sense, but for larger (and sparse) systems, iterative solvers are computationally beneficial.

Fixed point iterative solvers pass data between systems until convergence is reached. They do not require gradient information. You can imagine component A giving data to component B, and then B gives data to A, and this process repeats. Fixed point solvers are maybe the most intuitive because limited mathematics are required to understand how convergence occurs.

For any solver setup, a hybrid or nested approach is also possible. What I mean by this is that you could perform n iterations of Gauss-Seidel before using a Newton solver to really drive down the residual. Additionally, a nested solver hierarchy might be advantageous based on the amount of coupling and complexity within your model. [[Nested nonlinear solvers]] goes into more detail about those setups. For computationally expensive problems that you solve often, it's useful to determine the best solver setup, which might include hybrid approaches.

## Linear solvers
In practical terms, linear solvers obtain the gradient information for your system by solving the linear system $Au=b$. Please do not solve this system by finding the inverse of $A$ because it is computationally expensive. Instead, if you want to solve the system directly, use one of the factorization methods from the solver tree figure. For large and sparse linear systems, iterative methods are usually the best option.

You only need a linear solver if you need gradient information for your system. This would be relevant if you are performing gradient-based optimization or using a nonlinear Newton solver as Newton's methods require derivative information. When in doubt, include a linear solver in your system to avoid headaches when solving nonlinear systems.

## Nonlinear solvers
Solving general nonlinear systems is no easy feat and is the cause for many issues during the MDAO process. Due to the coupling within complicated system models, nonlinear solvers become extremely important to understand and implement correctly. To be clear, if you have any sort of coupling -- explicit components that are backwards coupled, or any implicit components -- you need a nonlinear solver. If you do not have a solver converging your model, your output data will be wrong as it will not capture any interdisciplinary backwards coupling.

As noted in Section 3.6 of *Engineering Design Optimization*, nonlinear methods can solve any algebraic system of equations that can be written as $r(u)=0$. Because of this, nonlinear systems range from simple to solve to extremely challenging. An example of a tough system to converge is the performance of a turbine engine due to the intricate and coupled elements within the system.

In general, I'd suggest starting with a Newton solver and seeing if it can converge your system. If you do not have efficient derivatives, then nonlinear block Gauss-Seidel is probably the best starting point. From there, you can tinker with solver settings based on your model's convergence.

## Solvers within OpenMDAO
OpenMDAO has a wide array of nonlinear and linear solvers implemented for you to use, as [listed on this doc page](https://openmdao.org/newdocs/versions/latest/features/building_blocks/solvers/solvers.html). One of the most beautiful facets of OpenMDAO is that it tracks the gradient information through any linear or nonlinear solver so you don't have to worry about what including these solvers mean for your gradient computation complexity. Instead of you needing to unroll a while loop and track the derivatives throughout, OpenMDAO does this behind the scenes when converging your systems.

When creating a model in OpenMDAO, assume that you need both nonlinear and linear solvers until you confirm otherwise. Looking at an N2 diagram (more info at [[Using N2]]) will help you determine if there's coupling within the model and where solvers should be located to resolve that coupling. It's easy to accidentally only put a nonlinear solver on your model and not solve the linear system, which leads to bad derivative information. Avoid this problem by either converging your linear system or verifying that a solver is not needed. 

### Types of nonlinear solvers within OpenMDAO
You have access to [Gauss-Seidel](https://openmdao.org/newdocs/versions/latest/features/building_blocks/solvers/nonlinear_block_gs.html) and [Jacobi](https://openmdao.org/newdocs/versions/latest/features/building_blocks/solvers/nonlinear_block_jac.html) nonlinear solvers within OpenMDAO. Generally, you should use Gauss-Seidel because it has better convergence properties than Jacobi. Use Jacobi if you are parallelizing your model across the solve.

OpenMDAO has both [Newton](https://openmdao.org/newdocs/versions/latest/features/building_blocks/solvers/newton.html) and [Broyden](https://openmdao.org/newdocs/versions/latest/features/building_blocks/solvers/broyden.html) solvers as well. Broyden is a quasi-Newton approach that approximates the inverse of the Jacobian instead of solving the linear system, which might reduce computational cost in some cases. That being said, you should probably start with a Newton solver if you're not sure about which to use. 

When using a Newton solver, it might be helpful to first perform a single iteration of Gauss-Seidel to help give your model better initial state guesses. OpenMDAO has a built-in option for the Newton solver called `solve_subsystems` that if set to `True` will iterate through the system once before beginning the Newton solve, resulting in a hybrid solver approach. I generally recommend setting `solve_subsystems=True` as it might result in more robust convergence, but it certainly varies problem-to-problem.