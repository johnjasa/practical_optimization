tags: #optimization #high_priority 

Sometimes confusing to novices and experts
"Bounds" vs "constraints" should be clear

## Main message
Bounds limit what design variable values can be set by the optimizer and do not require evaluating the model. Constraints are set on the outputs from the model and require evaluation.

## When and how to set bounds
- when you want a DV to stay within a certain region, set lower and upper bounds for it
- depending on the optimization algorithm, it will never exceed those bounds (TODO: verify which ones)
- these bounds might be set by the physical limits of your system, manufacturability, or artificially based on where you're interested in the design

## When and how to set constraints
- constraints are on outputs of the model
- there are linear and nonlinear, as well as inequality and equality constraints
- you *could* formulate a DV bound as a linear constraint, but that's not smart
- these can and will be violated by the optimizer during its process
- if there are values that cannot be exceed **ever** in your model or it breaks, special care must be used; a constraint is not enough. You'd need some sort of error handling as well.