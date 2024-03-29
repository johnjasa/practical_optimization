tags: #model_construction

- [x] main message created
- [ ] main message verified with someone
- [x] info outlined
- [x] info fleshed out
- [x] visuals ideated
- [x] visuals developed
- [x] lecture recorded
- [x] video produced
- [x] video uploaded
- [ ] 1st round feedback received
- [ ] video refined based on feedback
- [ ] video reuploaded
- [ ] re-render and reupload

- [ ] notebook created
- [ ] notebook text completed
- [ ] notebook examples completed and checked

Visualizations:
- [x] Show a web of groups and components (matches OM docs) then transform them into the nested block diagram
- [x] Manim animation showing blocks that live within a bigger block, zoom in and show other blocks, then zoom out and show all the blocks at the same time, green for groups and blue for components, show a heterogeneous system with groups and components at different levels
- [x] make an N2 matching the version we just showed
- [x] The middle-ground is best; show an N2 for that as well
- [x] Show an OAS or WISDEM system where some of the groups correspond to physical systems
- [x] get OAS N2
- [x] get WISDEM N2
- [x] get pycycle N2

I had a vision in the evening about a better way to discuss how to draw bounding boxes on models
I made a draft video and got Justin's feedback
Basically, the lesson is a bit too vague and doesn't have clear messages
I will put it aside for now as it's not the most critical lecture
This was on [[2022-07-28]]


## Main takeaway
You should intelligently group components and subgroups in an intuitive way that makes computational or physical sense.

## What is the best size for groups?
The best way to set up components, groups, and groups of groups, is quite subjective. Depending on the problem you're solving, it might make sense to have just one top level group if it is a small problem. However, most complex optimization problems very quickly become nested groups of groups.

PyCycle, for example, has many components that live inside of each of its groups. These groups are often then nested within other groups. This allows for a more clear delineation of engine components and setting them up to talk to each other.

## Usually top-level groups are physical systems or disciplines
An example within aircraft would be having a top-level group for the wing, thermal systems, propulsion, weights, etc. For a wind turbine you might have blade, tower, nacelle, foundation groups. Within these top-level groups you can have subgroups that have more delineation for the actual computations.

There's a subtlety in terms of how people consider groups. Sometimes it might make sense to group all analyses for a given discipline at the top level, or it might make sense to have the physical systems represented at the top level. For instance, should you have an aerodynamic representation of the wing, fuselage, and tail of the airplane all within one group called "Aerodynamics"? Or should you instead have an "aerodynamics" subgroup inside each top-level group called "wing", "tail", and "fuselage"? There is no definite answer and the best practice varies based on the complexity and purpose of your model.

## How many groups are too many?
It's tough to say what the correct number of groups (or subgroups) is. If you have a complex model, such as lot of engine models from PyCycle, you can expect nested groups up to 7 layers deep.

There are not significant computational advantages to using many components in OpenMDAO versus few components for the same calculations. The overhead behind the scenes is largely independent of the number of nested groups at the OpenMDAO level. That being said, complex models are generally challenging to solve, but one of OpenMDAO's goals is to not create an unnecessary bottleneck due to how you organize the model.

## Make reusable groups
A smart software design idea is to purposefully created groups to be reusable across different models and design problems. For instance, an airfoil analysis module might be useful within an airplane wing analysis, the propeller performance module, a wind turbine blade analysis, or a sailboat's hydrofoil optimization. If you can make a single group meet all of your needs for a given design paradigm, that's fantastic. Sometimes it's not even that complex; maybe a group can be useful for an aerodynamic optimization and an aerostructural optimization. You might as well use it for both. Don't spend unnecessary effort to rework your code, but do reasonably think about where this group would be useful.

One way to make reusable groups without thinking about it too much is to use variable names that are generalizable and useful to the group. By naming variables too specifically, you might be pigeonholing your group usage unnecessarily.