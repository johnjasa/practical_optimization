tags: #model_construction #high_priority 

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

Came up with [[Caroline Kuhnle]]
Normal shock equations
Can choose to get an explicit solution
Or can get an implicit relation
Vary parameters downstream so those balances are maintained
Reminiscent of pycycle

Existing docs on implicit components are confusing

Helpful to do different approach to see how you'd use the different objects
This was also a more hands-on intro to OOP
XDSM reasonable but you can also do them by hand


I need to give this very good thought


## Main message
You can formulate any part of a system as an explicit or implicit system. Explicit systems are generally easier to solve but implicit systems are necessary and helpful to correctly model physical phenomena.

## Implicit vs explicit components
- explicit is any time you can write a series of expressions that compute the outputs based on the inputs
- this is like y=ax^2 + bx
- implicit is like y = ax^2 * y
- sometimes you can write things that look like an implicit component as an explicit component

## When to make an implicit model
- usually if there's a real loop in the physical system this is a good hint for an implicit system
- also whenever there's some dependence on surrounding values or residuals

## An implicit system and equivalent explicit system
- this was a great idea from Jennifer
- Having a 1-on-1 about what an implicit component is
- Also do two explicit components in a group
- Show how they're similar and different

## How to use implicit models correctly
- you have to resolve the implicitness by using nonlinear solvers
- you generally want to put the solver at the lowest level for different loops
- you may need a nested system of solvers, like [[Nested nonlinear solvers]]