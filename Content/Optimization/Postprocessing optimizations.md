tags: #optimization #high_priority 

- [x] main message created
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


# Main message
Postprocessing and understanding optimizations is paramount to being a successful MDO practitioner. Optimizing is just half the battle -- understanding the resulting design and how the optimizer got there is the other half.

## What is postprocessing?
- looking at the DVs, cons, and obj histories across iterations
- checking out the optimizer logs and convergence histories
- visualizing the final design or checking to make sure it makes physical sense
- maybe even running the resulting design at higher fidelity

TODO: add plot from CaseViewer showing the DVs etc for iterations

## Built-in tools for postprocessing
- case recording and reading
- Solver vs driver vs system case recording; which do I use?
- Course can be distilling the why of case recording
- Docs could be refreshed on case recording
- discuss the CaseViewer and visualization

TODO: add simple optimization with case recording example
TODO: show a CaseViewer example interactively in the notebook
TODO: go through the CaseViewer viz in the video

## Other ways to postprocess
- can also use OptView in pyOptSparse if you want
- honestly you could just use the debug_print function
- also if your model produces any output files you can check them out along the way

TODO: get a video of OptView
TODO: make a notebook example using debug_print

## What to look for when postprocessing?
- look for DVs right at the bounds; see if those are physical bounds or if you can open them up
- see if constraints aren't being satisfied and what trade-offs are occuring
- the actual path of the optimizer doesn't physically mean anything. don't read too much into it except for debugging. what I mean by this is that if the optimizer takes one path over another it doesn't mean one design is better than the other; just the optimal design matters
- check out the order that the optimizer changes DVs. The DVs that the optimizer changes in the beginning probably have the biggest effect on the design. The last ones it changes usually have the smallest sensitivities, at least for gradient-based optimizers. This is also related to [[Basic scaling techniques]]

TODO: show example case where the DVs are right up against the bounds but the constraints aren't satisfied
TODO: show two different optimization cases that start at different places but go to the same result; do the paths matter? no
TODO: show an optimizer that changes certain DVs first, maybe wind turbine changing rotor diameter vs small scale airfoil design
TODO: visualization of the optimization history is super helpful for GASPY, grab an example from Jennifer
