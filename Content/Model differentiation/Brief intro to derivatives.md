tags: #differentiation 

## Main message
Derivatives are necessary to effectively guide gradient-based optimizers and Newton solvers to the correct answers.

## Types of derivatives
Relevant for model-based systems engineering there are two subcategories of derivatives; partial and total derivatives (sometimes just called "partials" and "totals").

Partial derivatives are any measures of some output from a subsystem changes with respect to its inputs. In OpenMDAO terms, this would be the sensitivity of the outputs with respect to the inputs of a component.

Total derivatives, on the other hand, are the combination of multiple partial derivatives into a single gradient. An example here would be the outputs of a full system with respect to the design variables. Total derivatives for a system are computed automatically by OpenMDAO when the partials for the components within that system are provided.

## Benefits and costs of using derivatives
Implementing derivatives for a model takes developer cost to lower computational cost. Specifically, there is some development time needed to either compute derivatives by hand or use algorithmic differentiation, for example, but the work invested there will make solving future optimization problems less computationally expensive.

Efficient computation of derivatives will unlock designs that would not be possible otherwise. This is the impetus behind the entirety of OpenMDAO -- to make hard problems easy and to make previously impossible problems hard. One of the main ways that OpenMDAO enables that is through efficient computation for gradient-based optimization.

It may not always be necessary to compute derivatives for models. Generally we strongly suggest using gradient-based optimizers with efficiently-computed derivatives due to the computational benefits (see: [[Why to use gradient-based optimizers]]). That being said, you *can* compute derivatives via the finite difference (FD) or complex-step (CS) methods and still use gradient-based optimization at a dramatically reduced developer cost. However, you face an increase in computational cost that scales with the number of design variables, so highly dimensional problems are generally off the table using these methods.

For extremely low-cost models or low-dimensional design problems, it may not be worth it compute derivatives. For instance, if one analysis of your model takes 0.01 seconds, and computing the derivatives would take 16 person-hours, it may make the most sense to use gradient-free or finite-differenced gradient-based optimization methods. This trade-off varies on a problem-by-problem basis, so developers and modelers should take special care to consider how often their models will be used in design optimization.


