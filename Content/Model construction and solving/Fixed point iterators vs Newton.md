tags: #model_construction

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
The type of solver you should use for your model depends on the cyclicity, computational cost, convergence, and I didn't mean to use only words that start with C, yet here we are.

## Fixed point iterators
- FPI or nonlinear block gauss seidel
- these simply run one part of the model then the next in a cyclical fashion
- imagine a point bouncing between two lines (but it can be hyperdimensional) until convergence
- useful because they don't require derivatives
- may be slightly more stable than Newton's methods
- allows for Aitken relaxation

## Newton's method
- check out [[Newton's method math]] and Eytan's video for more info on the basics
- but the idea is that we use gradient information to help solve the system
- this is great for more complex systems
- however you need a nice guess for them, usually
- sometimes a hybrid approach might be good but only for really sticky cases

## When to use what
- I'd say at first pass, try a FPI
- If that doesn't converge your system or the performance is bad
