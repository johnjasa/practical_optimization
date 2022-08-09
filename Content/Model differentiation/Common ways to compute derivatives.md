tags: #differentiation 

- [x] main message created
- [ ] main message verified with someone
- [x] info outlined
- [x] info fleshed out
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

Viz ideas:
- [ ] simple finite difference manim visual
- [ ] more complex FD visual where you show subtractive cancellation. 
- [ ] complex step is basically magic. some metaphor about how much a peanut means to a housefly vs what it means to an elephant. or how much 5 nanograms of silica matters to a processor vs a meteor
- [ ] partial deriv computation by hand, showing the power rule or similar
- [ ] walk through Jax or similar visually

## Main message
There are many ways to compute partial derivatives: finite-differencing, complex-step, analytically by hand, or through algorithmic differentiation. The best method depends on your problem formulation, but the best implementation usually involves an intelligent mix of these methods.

## Finite difference
Finite difference (FD) is the simplest and least invasive way to compute derivatives, but it does not produce accurate or efficient results.  FD is when you evaluate a system at a certain point, then perturb that system and reevaluate it. The change in function value is then divided by the perturbation to get an approximated slope or derivative of the system. This is shown mathematically as:

$$\frac{\partial f}{\partial x} = \frac{f(x+h) - f(x)}{h} $$

where h is the perturbation size. The accuracy of the FD approximation varies with h and is highly dependent on model, problem formulation, and location within the design space. Martins and Ning Sec. 2.2 (TODO add correct section) discuss this in great detail.

For the purposes of this course, I'm going to try to dissuade you from using FD. It is tempting because it works for any and all models, even when treated as a blackbox. However, it scales very poorly with the number of design variables and does not produce reliably accurate gradients. Additionally, as model complexity increases, FD becomes computationally intractable. For instance, we are solving coupled design and mission optimization problems at NASA Glenn with hundreds if not thousands of design variables. Using FD would make this computationally impossible.

That being said, if you're just starting with a blackbox model and need to approximate derivatives without adding any developer cost, FD is the way to go. If you have knowledge about or access to the model and know that it is able to handle complex numbers, you should use the complex step method.

TODO: add total derivative FD example in OM
TODO: add partial derivative FD example in OM

## Complex-step

The complex-step (CS) method is a much more accurate version of the FD method. It works by perturbing a system in the *complex* plane to obtain derivatives. Because the perturbation occurs in a plane orthogonal to the real values of the function, the outputted float representations of the derivative are not hindered by the limitations of subtractive cancellation. This allows CS to produce exact derivatives when using a small enough step size, such as 1j*1.e-40j.

$$\frac{\partial f}{\partial x} = \frac{f(x+ ih) - f(x)}{ih} $$

Please check out the section in the MDO Book (TODO add link) or the complex-step paper by Martins in 2004 (TODO add link) for more theoretical details.

The biggest practical consideration is that you need a complex-safe model. What I mean by this is that your model has to fully propagate complex numbers through it correctly. If you have an external solver in Fortran or C, for instance, and it's assuming all numbers are real-typed, then any perturbation in the complex space will not be reflected throughout the model. Thus, complex-step is best used on *graybox* models where we have some information about what's going on behind the scenes. If you're not able to verify if a model is complex-safe, try using the complex-step method as compared to FD to see if the derivatives are roughly the same, accounting for the inaccuracies introduced by FD.

TODO: add complex step examples in OM
TODO: mention that when you use ExecComps you are using CS under the hood and show an example

## Analytically or by hand
When you compute derivatives by hand you are paying high developer cost to reduce computational cost by obtaining exact derivatives. This is really where your understanding of calculus and differential equations comes into play. It's not necessarily easy to compute derivatives by hand, but if you know you're going to be performing many optimizations with a model or it will be used in many multidisciplinary studies, it's often quite worthwhile.

People have different best practices for computing derivatives by hand. Some people sit down with a pad of paper, others use WolframAlpha or another symbolic differentiation engine. All methods are valid as long as they result in accurate and efficient derivatives -- though that is no small feat.

Sometimes it's as easy as doing the power rule across a function; other times you have to do some pretty advanced tensor calculus. Depending on how you construct and set up your model, your derivative computations can be made easier to save your sanity. For instance, if you have one 1000-line component, it would probably be very challenging to analytically compute derivatives. However, if you have 10 100-line components, you might be able to more easily compute the partial derivatives for each of those smaller computation amounts. OpenMDAO will then combine the partial derivatives together behind the scenes, which is just fantastic.

I certainly can't cover all the ins and outs of computing derivatives by hand. It sometimes takes months or years of hands-on experience to get a good feel for computing derivatives of complicated models. That being said, many of our topics regarding model differentiation discuss this, especially [[How to structure your code to be easily differentiable]], [[Advanced ways to compute derivatives]], and [[How to avoid non-differentiable functions]].

TODO: show some very simple analytic derivs in OM

## Algorithmic differentiation
Algorithmic differentiation (AD) is also known as automatic differentiation. AD is where a computer does the differentiation for you based on code you provide for the model. This can be done via source code transformation or operator overloading (TODO: add links to resources).

Some programming languages and packages exist to help perform AD on your models, including tensorflow, Jax, Tapenade, Julia, etc (TODO: add links). It would be fantastic if AD was a cure-all reliable method of producing derivatives, but it often has limitations in terms of what code can be converted. There are many potential pitfalls, including code structure, variable use, cost of computing derivatives, lack of support for operations, etc. However, if AD works for your model, then you get the benefits of analytic derivatives without the huge developer cost! Isn't that great?

This is something that the OpenMDAO developer team has considered throughout its development, though it is not natively implemented in OpenMDAO.