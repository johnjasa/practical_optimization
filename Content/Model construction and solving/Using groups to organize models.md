tags: #model_construction


Examples:
- WISDEM wind turbine delineation
- OAS
- GASPy?

Visualizations include N2 and XDSM
Show the same model in different ways
Slowly phase in visualizations


## Main takeaway
You should intelligently group components and subgroups in an intuitive way that makes computational and hopefully physical sense.

## What is the best size for groups?
The best way to set up components, groups, and groups of groups, is quite subjective. Depending on the problem you're solving, it might make sense to have just one top level group if it is a small problem. However, most complex optimization problems very quickly get groups of groups.

PyCycle, for example, has many components that live inside of each of its groups. These groups are often then nested within other groups. This allows for a more clear delineation of engine components and setting them up to talk to each other.

## Usually you want your top-level groups to be a physical system or discipline
An example within aircraft would be having a top-level group for the wing, thermal systems, propulsion, weights, etc. For a wind turbine you might have blade, tower, nacelle, foundation groups. Within these top-level groups you can have subgroups that have more delineation for the actual computations.

There's a subtlety in terms of how people consider groups. Sometimes it might make sense to group all analyses for a given discipline at the top level, or it might make sense to have the physical systems represented at the top level. For instance, should you have an aerodynamic representation of the wing, fuselage, and tail of the airplane all within one group called "Aerodynamics"? Or should you instead have an "aerodynamics" subgroup inside each top-level group called "wing", "tail", and "fuselage"? There is no definite answer and the best practice varies based on the complexity and purpose of your model.

## How many groups are too many?
It's tough to say what the correct number of groups (or subgroups) is. If you have a complex model, such as lot of engine models from PyCycle, you can expect nested groups up to 7 layers deep.

There are not significant computational advantages to using many components in OpenMDAO versus few components for the same calculations. The overhead behind the scenes is largely independent of the number of nested groups at the OpenMDAO level. That being said, complex models are generally challenging to solve, but one of OpenMDAO's goals is to not create an unnecessary bottleneck due to how you organize the model.