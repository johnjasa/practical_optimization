tags: #lesson 

# Checklist for doing good optimization

## Main message
A systematic approach is needed to solve complex MDO problems and understand the results. This set of lessons provides a helpful checklist to follow.

## Optimization Checklists

Here are general checklists for before and after solving optimization problems.
The idea and outline of this checklist came primarily from MDO Lab researchers, including [[Sham]] and [[Neil]].

## General pre-optimization checklist

1.  **Write down a formal optimization problem formulation** (preferably in latex so that you can update and reuse it).

   - If you don't know what this is, see Prof. Martins' MDO `book <https://mdobook.github.io>`_.
   - See previous papers for examples (e.g., Table 2 in https://doi.org/10.2514/1.C034934).
   - This will include the objective function, the constraint functions, and the design variables (with bounds).
   - This will help make sure that you do not start solving the wrong problem.
   - Also related to [[Basic optimization problem formulation]] and [[Advanced problem formulation]]
   - Viz: optimization problem coming together, highlight the objective, constraints, and design variables

2. Think hard about whether a **simpler optimization problem can be solved first**.

   - e.g., before trying a twist and shape aerodynamic optimization, first try a twist-only optimization.
   - This approach of building up your optimization problem complexity will make it easier to troubleshoot and explain results.
   - Starting with cheaper test cases can also help with debugging (e.g., optimizing with a coarse mesh first).
   - If this is applicable, go through all the checklists for the simpler problems as well
   - Viz: Show a highly dimensional problem and then show a simpler one?

3. **Carry out some kind of verification (and validation when possible)** for your simulations.

   - Come up with tests to verify that the code is behaving as intended.
   - For validation, compare results to theoretical predictions, experimental data, or other trustworthy results.
   - Viz: V&V is necessary to trust the results
   - Also see [[Verification and validation]]

4. **Verify your gradients** (or hope that you get lucky and the optimization converges well). Options include:

   - manually comparing values with finite-difference and complex-step estimates
   - this is only if we're using gradient-based optimizers
   - SNOPT's finite-difference check printed in the SNOPT_print.out file (the default is a "cheap" test in one direction; see the `SNOPT guide <https://ccom.ucsd.edu/~optimizers/static/pdfs/snopt7-7.pdf>`_ for more options)
   - the ``check_partials`` method if using OpenMDAO (just another convenient way to compare with finite-difference and complex-step estimates)
   - [[Checking your derivatives]]

5. Unless you have a good reason to do otherwise, **use scaling such that the design variable ranges and the values of the objective and constraint functions will be around 1** (this may not be applicable for all optimizers but definitely is for SNOPT, our most used optimizer).

   - This should help avoid unwanted behavior (e.g., difficulties converging; e.g., achieving specified tolerances when far from an optimum because of the scaling), but this is not a perfect strategy and further experimenting may be necessary.
   - With SNOPT, when the constraints are satisfied with this scaling strategy, the optimality criterion will reflect roughly how much the objective function can change.
   - This is related to [[Basic scaling techniques]] and [[Automatic scaling techniques]]

  6. **Double check your initial design**.

   - Make a checklist of important parameters and check them.
   - e.g., geometry dimensions and units, FFD control-point locations, grid spacings, etc.

7. **Check whether your design variables behave as expected**.

   - e.g., perturbing the FFD grid and checking the deformed shape of the surface
   - Viz: show a parameter sweep of results

8. **Check and note down the optimization tolerances being used** (or other termination criteria). This helps you verify that the optimizer converges as much as you need.

9. **Double check that your script reflects your optimization problem formulation.**

   - Make a checklist using the problem formulation from step 0 and check.
   - e.g., checking that the specified values for the design variable bounds are correct

10. **Check the optimization problem setup by running a couple optimization iterations** and examining the results.

   - e.g., check the number of design variables and constraints in the optimizer's output
   - Use `debug_print` at OpenMDAO


## General post-optimization checklist
1. What is the exit information (did the optimization problem actually converge or did it terminate prematurely)?
2. Are any of the design variables at their bounds? If yes, is that acceptable?
3. If the problem did converge, come up with and carry out sanity checks for the results.
4. If the problem did not converge, check if the analyses and gradient computations converged.

   - e.g., there may be analysis errors due to mesh failures or solver divergence
   - e.g., the analysis or gradient tolerances may be too large to provide the accuracy necessary to achieve the specified optimization tolerances

5. If the problem did not converge and there are no problems with the analyses and gradients, experiment with scaling and check the pre-optimization checklist again.
6. If the problem did not converge and you checked all the above, ask for help!

## Checklist for showing results 

Along with the plots and images that you consider relevant, include the following information:

1. Optimization problem formulation
2. Optimizer name, specified optimization tolerances (or other termination criteria), and scaling.
3. The termination information and the tolerances achieved
   - If using SNOPT, the exit code and its description (see :ref:`SNOPTGuide` for the common exit codes, and see the `SNOPT guide <https://ccom.ucsd.edu/~optimizers/static/pdfs/snopt7-7.pdf>`_ for more)
4. If using SNOPT, include the value of ``-log10(Max Dual infeas/Max pi)``.

   - This should give an estimate for which significant digit can be expected to change if the optimization could continue. (See the `SNOPT guide <https://ccom.ucsd.edu/~optimizers/static/pdfs/snopt7-7.pdf>`_ for more)

5. If design variables are at their bounds, which ones
6. The lists of checks you did for the `verification and validation`_ , `gradient`_, `initial design`_, and `design variables`_ items in the pre-optimization checklist
7. Which steps of the pre-optimization checklist were skipped and why