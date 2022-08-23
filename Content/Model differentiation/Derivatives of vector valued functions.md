tags: #differentiation #high_priority 

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

Diagonal, non-diagonal, sparse

When you're computing a Jacobian, what are the rows and the columns?
Determine a nice way or pneumonic or know
A picture
dF/dX means what?

## Main message
Derivatives of a scalar with respect to a scalar might be relatively straightforward. Derivatives of vector valued functions are not impossibly difficult. You can use intelligent matrix and array operations to facilitate the process.

## What are vector valued functions?
- anything where you have multiple inputs or outputs for a given quantity of interest
- these are extremely common in engineering models and should be assumed to be the norm
- in fact, this is a side note but even scalars are considered 1x1 arrays in OM

## Brief math theory of derivative arrays
- show the Jacobian as a 1x1 for a simple equation
- then show the Jacobian as a 1xn for a slightly different equation
- then show it for an nxm problem based on the inputs and outputs

## Example case implemented in OpenMDAO
- show a 2x3 example case
- walk through the derivative calculation in theory
- show the corresponding code and build it up by hand

## Sparsity in the Jacobian can be exploited
- exploited is maybe the wrong word; it's not like the Jacobian is hurt
- but basically, there's a common thing in engineering problems where only some of the inputs affect the outputs
- you can use sparse Jacobians to help reduce computational expense of computing derivatives here
- in the simplest cases, the derivative values are only non-zero on the diagonal
- you can get some pretty crazy sparsity patterns
- OpenMDAO has many tools to help you do this

## Derivative coloring can also help
- introduce the idea of coloring here
- but link to the partial and total derivative coloring lectures