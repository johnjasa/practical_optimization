tags: #optimization 

- [ ] main message created
- [ ] main message verified with someone
- [ ] info outlined
- [ ] info fleshed out
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

## Main message
There are a few broad categories of gradient-based optimizers, including SLSQP, SNOPT, IPOPT, and others.

## Prefacing context
There are a lot of gradient-based algorithms that I will not detail here, like [BFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) and the [augmented Lagrangian method](https://en.wikipedia.org/wiki/Augmented_Lagrangian_method) because there are other methods that are generally more useful. All methods described here are available in OpenMDAO.

## SLSQP
SLSQP is a sequential quadratic programming (SQP) method that is available in Scipy and pyOptSparse. It can handle arbitrary constraints and is the de facto publicly-available gradient-based algorithm. [Nocedal and Wright](https://link.springer.com/book/10.1007/978-0-387-40065-5) detail it well in their book and [Scipy has good documentation](https://docs.scipy.org/doc/scipy/reference/optimize.minimize-slsqp.html) on it as well.

If you're not certain about what optimization method to use, SLSQP is a great one to start with. If you find your problem isn't converging well, you can tweak some of its options or try a different optimizer, but its ubiquitous use makes it a good first optimizer.

## SNOPT
You can think of SNOPT as a slightly better optimizer than SLSQP for a subset of problems. [SNOPT is a commercial code](https://ccom.ucsd.edu/~optimizers/solvers/snopt/) that is an SQP method with a bunch of extra features. SNOPT is commonly used for highly complicated problems at NASA Glenn and in the MDO Lab. It is integrated into pyOptSparse and provides a good amount of problem and convergence information through its logging system.

SNOPT is highly customizable as it has a large number of user-controllable options. Hopefully you shouldn't need to tweak them too majorly, but if you do, the [SNOPT reference guide](https://ccom.ucsd.edu/~optimizers/docs/snopt/) will be your friend.

## IPOPT
[IPOPT](https://coin-or.github.io/Ipopt/) is an interior point method that is especially useful for some trajectory optimization. It can handle general nonlinear constraints and is available in pyOptSparse.