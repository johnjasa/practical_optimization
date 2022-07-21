tags: #model_construction

- [x] main message created
- [ ] main message verified with someone
- [x] info outlined
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
The N2 diagram is a fantastic interactive tool to understand and debug your OpenMDAO models. If you're wondering how systems are organized, connected, or solved, an N2 is for you.

## Brief intro
This lecture and notebook will not be focused on introducing the N2 and how it works. There are already resources available for that (TODO: add links to resources here, like the YT video, any docs, etc). That being said we need to cover some basics, like how to mouse over things and what they mean. The truly best thing is that OpenMDAO produces N2 automatically for your models.

## Debugging connections using N2s
- look at the off diagonals
- mouse over the names that you're interested in
- click to keep connections and look around
- look at which ones are red or come from IVCs; are they correct?

## Debugging grouping using N2s
- take a look at your components and groups. are they all where they should be?
- are there places where you have a nonlinear solver around a group that doesn't necessarily need one? also see [[How to debug solvers]] and [[Nested nonlinear solvers]].
