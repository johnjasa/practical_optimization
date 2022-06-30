tags: #optimization 


## Main message
Use gradient-free optimizers when the design space is noisy or discontinuous, there are multiple optima, the computational cost for the model is very low,  or when you cannot efficiently compute derivatives.

## Noisy and discontinuous design space
- show an example in 1 or 2D what I mean by noisy
- and what I mean by discontinuous
- this inherently includes mixed integer problems -- how would you get the derivatives of a boolean?

## Multimodal problems
- gradient-free algorithms don't automatically solve multimodal problems better than gradient-based ones
- that being said, there are a slew of algos (list) that are focused on global optimization
- it is a common misconception that gradient-based algos shouldn't be used for multimodal problems; just do a multistart

# Very cheap models
- if it takes seconds to run a few iterations of your model, you can use a gradient-free optimizer and be fine
- but this is only if the design space is quite small or lower dimensional

## When you can't compute derivatives
- admittedly, it's generally developer expensive to compute efficient derivatives for complex models
- if you want to get an optimization running without worrying about derivative computation of any sort, even FD or CS, you can just let it rip with gradient-free methods