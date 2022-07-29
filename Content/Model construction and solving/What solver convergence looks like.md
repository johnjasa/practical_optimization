tags: #model_construction 

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
- [ ] notebook text completed
- [ ] notebook examples completed and checked

Viz ideas:
- [x] XDSM showing no coupling; feed forward system
- [x] XDSM or N2 showing backwards coupling
- [x] XDSM or N2 showing implicit model and component
- [ ] manim line plot showing convergence for the solver, use a real case or example from OM; NLBGS, Newton
- [x] show nested solvers and what convergence looks like there

## Main message
A system is converged when the residuals are close to 0 within a tolerance. How this is achieved depends on what solver you use, but generally you want your residuals to decrease as computationally quickly as possible.

## The basic idea of convergence
Solver convergence means that the system's coupling or implicit relationships are resolved to the specified tolerance. Basically, the states (variables) within the system are at steady-state values for the given inputs. This mean that the outputs of the systems correctly correspond to the inputs. For any solver, we want the residual values of the states to be 0.
$$ R(x) = 0 $$ but really it's
$$ R(x) < \text{tol} $$
where $\text{tol}$ is some number that is reasonably close to 0, maybe 1e-4 or 1e-8 or some other small number based on your problem.

Convergence is relevant for both nonlinear and linear solvers. In oversimplified terms, you are converging the states of the system for nonlinear solvers whereas for linear solvers, you are converging the derivatives of the system. See [[Nonlinear vs linear solvers]] for a more detailed look. It's easier to think about nonlinear solvers converging states for a lot of people, so I'd suggest imagining those instead of linear solvers for this lesson.

Your solver might converge part of your model sooner than another part due to the magnitude of the states and residuals. An example would be a solver that's converging the mass of an aircraft as well as its angle of attack. Without any scaling, the mass is a much larger magnitude than the angle of attack. The solver would prioritize resolving the mass residual much more than the angle of attack. This is also a motivating case for scaling your state variables when using complicated solver setups. This is a different but related topic to optimizer scaling.

To be clear, the idea of solver convergence is different than that of optimizer convergence. They both use the word convergence and a similar mathematical idea, but practically they're quite different. You can think of solvers as a certain type of optimization; for a solver you're trying to get the residuals to 0, but for an optimization you're trying to find where the gradients are 0. See [[Newton's method math]] and [[Unconstrained optimization using a Newton solver]] for more details and a more mathy view.

If your model is explicit feed-forward, in that there are no feedback loops or implicit states at all, you do not need a nonlinear solver or a notion of solver convergence. Most complicated engineering models have some sort of feedback. If you're not certain about the nature of your model, see [[Using N2]] on how to visualize and better understand you feedback loops.

## How to tell when something is converged
Determining when something is converged might be challenging. It fully depends on the problem you're solving and what you're doing with the results. If you're performing gradient-based optimization of high-fidelity CFD, you generally want a pretty tight tolerance. If you just need rough numbers or large-scale trends for an analysis, you might be able to get away with a looser tolerance. [[What solver tolerance should I use]] goes into much more detail about this.

## Convergence in the terminal
In OpenMDAO, solvers print out their convergence state based on their `iprint` value. You should generally have solver convergence printing on and logged to a file when doing analysis and optimization. This allows you to determine how a system is converging and how it's meeting the tolerances you've set.

Those two numbers are the *absolute* and *relative* residuals, respectively. You can set the tolerance for both of these values and accept convergence from either metric. There could be a system where you care about things on the order 1e10 or on the order 1e-5, so those relative and absolute tolerances might greatly differ.

http://openmdao.org/twodocs/versions/latest/basic_user_guide/multidisciplinary_optimization/sellar.html
https://openmdao.org/twodocs/versions/latest/features/debugging/debugging_solvers.html
http://openmdao.org/twodocs/versions/latest/features/core_features/controlling_solver_behavior/set_solvers.html
http://openmdao.org/twodocs/versions/latest/features/core_features/controlling_solver_behavior/solver_options.html

## Closing message
Converging a system means that all coupling and implicit interactions have been resolved. The best solver settings and what "good" solver convergence means are highly problem dependent.