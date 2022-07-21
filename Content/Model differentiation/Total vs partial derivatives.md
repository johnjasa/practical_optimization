tags: #differentiation

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
You need to tell OpenMDAO how to compute the total derivatives if you want to do gradient-based optimization. You can do this by specifying partial derivatives, requesting FD on the subsystem level, or using FD on the full system.

## What are total derivatives?
- derivs for the full system front to back
- we *technically* only care about functions of interest wrt DVs, but it makes sense to provide derivatives for all inputs and outputs of your model
- total derivatives are the regular d, not the curly d

## What are partial derivatives?
- these are just the in between derivatives
- they're the easier ones to compute
- ignore everything except the inputs and outputs you care about for that case
- happens on the component level and OM slaps them together

## You can compute total derivatives using a mix of partial derivative computation methods
- OM allows you to use any arbitrary mix of derivative computation methods you want for the system, subsystems, or even components
- whatever is most efficient or easiest for your problem and use case is what you should use
- 