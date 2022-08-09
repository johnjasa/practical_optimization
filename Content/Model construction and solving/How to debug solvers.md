tags: #model_construction #high_priority
related:
[[What solver convergence looks like]]
[[Types of solvers and when to use them]]

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
- [x] flash up Martins and Ning's categorization of solvers again
- [x] show the initial states vector as 0 -> ? -> converged values
- [x] highlight how to set_val in OM?
- [x] get a bad OAS case with huge residuals increasing
- [x] a wing that you accidentally make way too bendy (show wing, a force vector, maybe the elasticity)
- [x] notebook with a solver where you just need more iterations to get convergence

Feedback:
- [ ] briefly describe solve_subsystems and link to a more in-depth explanation
- [ ] bring up in section 2 that the solution might lie outside the bounds; this happens often in GASPy. maybe mention this during the checklist too
- [ ] Justin wants to see manually trying to converge
- [ ] also suggests showing the residual filter on list_outputs to reduce noise in the prints
- [ ] at 6min, 58 seconds you repeat the same audio "maybe I have something that isn't connected but it should be connected"


## Main message
Optimizers often push systems to their limits of multidisciplinary analysis, so sometimes solvers don't converge. You can follow a series of debugging steps to determine why this is and implement a solution.

This lesson will be quite focused on OpenMDAO-specific solvers, but the ideas are extensible to any sort of setup.

## What types of solvers are you using?
Before hashing out the debugging steps below, I highly recommend critically thinking about the type and combination of solvers you are using. Which types of solvers you're using greatly impact the debugging process. For instance, if you have a system without efficient derivative computation and you're using Newton's method with finite-difference approximated derivatives, convergence might suffer due to inaccurate derivatives. However, fixed-point iteration methods don't use derivative information, so that would not be relevant.

On the linear side of things, if you have a large and sparse system it might not make sense to use a direct solver. If you're facing convergence issues or large computational costs, switching to an iterative Krylov-based solver might be beneficial.

All this to say, give some thought to what solver you're using. Don't just copy-and-paste your same setup from a different problem without considering the problem you're trying to solve (trust me, I've done that all too often).

## Should you expect convergence?
This is another good question to ask yourself before going down the rabbit hole of debugging solver convergence. It's too easy to throw a lot at the solver and expect it to work a miracle. There are some (many!) problem setups that can't be solved.

Imagine you have a system with all its states starting at 0 because you haven't provided any reasonable initial guesses. I've done this a lot. Sometimes you don't know what a good state value would be or are just using the defaults. But asking a solver to determine these states without starting it from a reasonable location is a recipe for non-convergence.

Another case when you might not get convergence is when you ask a solver to calculate something from a physical setup that exceeds the model's limits. An example would be an aircraft wing that is experiencing a load *much* larger than its design load. Realistically, the wing would break. But in solver terms, it probably can't find a reasonable converged value for the displacement of the wing based on the large forces. This would result in the solver residuals "blowing up," or becoming unreasonably large and certainly not converged. One time I accidentally set up a wing and provided its stiffness to 1.e-9 what it should've been because I was thinking it was in GPa instead of Pa. This made an extremely bendy wing and the solver could not converge *any* loading I gave it.

So, think about your system! Do some back of the envelope math and order of magnitude checking to make sure that you're using reasonable numbers and inputting reasonable analysis conditions. Sometimes it's easy to not set up a solver for success and usually it's an initial guess or analysis condition problem.

## Checklist for solver debugging (in OpenMDAO)
This is radically simplified and has a lot of subtlety and nuance removed. Additionally a different order might make more sense for a particular problem given the computational cost, derivative implementation, or importance of how the solvers are failing. The last few suggested actions' order can definitely be swapped around depending on which is easier to implement for your model.

0. If you can computationally afford it, **try more iterations first**. For cheap problems this a no-brainer. For something that involves more cost, like medium- or high-fidelity applications like structural dynamics or CFD, increasing the number of iterations is probably not the answer. If your [direct linear solver](https://openmdao.org/newdocs/versions/latest/features/building_blocks/solvers/direct_solver.html) is failing you can't increase the number of iterations (because there are none), but you might need to use an iterative preconditioner on the linear system.
1. **Try using [solver debug printing in OpenMDAO](https://openmdao.org/newdocs/versions/latest/features/debugging/debugging_solvers.html)**. This is a very comprehensive way to view what the solver is doing, how the state vector is changing, and the values of the inputs and outputs in the system trying to be solved. A quick sanity check by looking over those values and their magnitudes can often reveal how something is going wrong in the model. For instance, sometimes I thought a value coming in was in megawatts but it was actually coming in as watts. With the debug printing on I very quickly saw that I was trying to solve a system with states that were 1.e6 different than what I was expecting and could then change my setup.
2. **Check your data connections within your model.** Using solver debug printing might reveal some values are not what you expect. This might be because those variables are not hooked up in your model correctly. You can using the N2 diagram ([[Using N2]]) to visualize your connections or the `openmdao view_connections model.py` command-line option to see a text output of your connections. Verify that all of the variables are connected as you expect.
3. **Try improving your initial guess for the state values.** This is helpful for all solver types, but especially Newton-based methods. You can see if your guess is better or worse by examining the 0th iteration residual when your solve starts. If your initial residual is huge compared to the tolerance you're asking for and the solver cannot converge the system that far, try to intuitively set up a better initial states vector using your understanding of the physical system you're modeling. For example, in the case of engine modeling, this means having a reasonable guess for the air mass flow rate through the engine based on the flight condition you're evaluating.
4. This is only for fixed-point iteration methods, like nonlinear block Gauss-Seidel. If your solver is not converging, **try adding Aitken relaxation** by setting the `use_aitken` solver option to `True`. This is especially helpful for tightly coupled models.
5. This is only for Newton methods; [consult this fantastic doc page](https://openmdao.org/newdocs/versions/latest/features/debugging/newton_solver_not_converging.html) which has more detail and more steps for your Newton solver debugging.  First **check your linear solver** to make sure it is converging the derivative values correctly. Because Newton methods depend on the derivative values, if your linear system provides incorrect gradient information it can cause your nonlinear solver to fail. If your Newton method isn't converging, **try adding a linesearch**, such as an [ArmijoGoldstein linesearch](https://openmdao.org/newdocs/versions/latest/features/building_blocks/solvers/armijo_goldstein.html).
6. This might take more time to implement, but **try reorganizing your model to minimize the amount subsystems contained within the solver** (if you haven't already). By having only the absolutely necessary subsystems within a solver loop you can drastically reduce computational cost compared to having solvers that iterate across groups unnecessarily. Anecdotally, we once improved speed of a code about 25x by changing where the solver was located within the model hierarchy, which allowed us to use more iterations and then reach convergence. This doesn't directly help convergence but instead allows you to iterate through debugging methods much more quickly.
7. This also might take a bit of time to implement, but **try using a nested solver hierarchy.** If you're having issues converging a complicated system, solving smaller subsystems and passing those solved systems up into the larger system might fix your problem. Unfortunately, this might introduce increased computational cost, but it should hopefully increase the robustness of your analysis. [[Nested nonlinear solvers]] goes into much more detail about this.
8. **Try removing some states from the solver loop.** This might seem counterintuitive but I suggest "freezing" some of the states so that they do not change in the solver loop. This will allow you to determine if there is a specific subset of states that is causing the solver to fail. A physical example would be in the case of floating offshore wind turbine design. Consider the multibody dynamics solver -- the thing that resolves how the wind and waves moves the turbine blades, affecting the generator, tower, and floating platform. If you "turn off" the waves (treat the wind turbine as land-based) so that they have no effect on the system, you effectively remove the states associated with that motion. Maybe then your system will converge and you know that you need to focus on the effects introduced by the waves. It greatly helps if you build your problem up piece-by-piece, solving each subpiece as you go along, so you can better understand if any additional physical considerations are causing convergence issues.