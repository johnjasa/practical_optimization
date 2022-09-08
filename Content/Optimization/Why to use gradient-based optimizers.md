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

Visualizations:
- [ ] show the famous plot and what it means
- [ ] show a SNOPT print file and highlight what the columns mean

## Main message
Gradient-based optimizers are the most efficient way to explore highly dimensional design spaces and find optimal designs.

## Gradient-based optimizers are quite efficient
Gradient-based optimizers intelligently explore the design space. They use both function and gradient information to traverse the space. When paired with efficient derivative computation methods, they work quite well for highly dimensional problems whereas other methods greatly suffer from the "curse of dimensionality".

Compared to gradient-free algorithms, gradient-based ones generally take much less time and fewer iterations to reach an optima. Especially when using efficient gradient computation methods, such as analytic or automatic differentiation.

## Mathematically, it's helpful for optimization
Gradient-based optimizers have mathematically sound termination criteria based on the curvature of the design space at the optima. Without getting too much into the math, know that gradient-based methods have provable convergence with some caveats, which is not true for gradient-free methods. 

Because of the knowledge of the curvature of the design space available, convergence is more easily understood. What I mean by this is that you can trace the path that the optimizer took while solving the problem and understand how the optimizer is converging. This will allow you to fine-tune your problem for future cases to reduce overall computational cost. If you dig into the optimizer log files, you can often debug your problems more quickly by examining the convergence metrics like optimality and feasibility.

## Considerations
When using gradient-based optimizers there are a few considerations, some of which were discussed in [[When to use gradient-free optimizers]].

Gradient-based optimizers, as you might've guessed, rely on gradient information to converge. By definition, this means that they are limited to solving continuous (non-discrete) problems. If you absolutely have to have discrete design variables, then you cannot use gradient-based optimizers off the shelf. That being said, it's often more beneficial to use gradient-based optimizers with different permutations of your discrete variables instead. This usually results in a set of design spaces that you can traverse in a reasonable amount of time.

Another consideration is the fact that multiple starts may be needed to better explore the design space. Gradient-based optimizers generally converge to local minima, which may be your desired behavior. However, if you have a multimodal function you should use multiple initial designs when using gradient-based optimizers. This will allow the different optimization runs to converge to different minima. Based on the final objective values from each of those optimizations you can select your most optimal design, which may be the global optimum.