tags: #model_construction

Progress:
- [x] main message created and verified with someone
- [x] info outlined
- [x] info fleshed out
- [x] visuals developed
- [x] lecture recorded
- [x] video produced
- [x] video uploaded
- [ ] 1st round feedback received
- [ ] video refined based on feedback
- [ ] video reuploaded
- [ ] re-render and reupload
- [ ] notebook finished

Feedback:
- [ ] face distracting on screen
- [ ] early simple XDSM diagram center then re-center
- [ ] around 3 minute mark the y output could be more clear that it's not just for the optimizer, but for anything
- [ ] around 6:51 aerodynamic loads should be differently named with caps
- [ ] agree with bret about presenter box being a distraction.. eyes are drawn away from the content.. it's not the face (human or owl..) but the motion/activity that steals focus.. (found myself noticing edit points, reflection in glasses, etc.)
- [ ] could pare down the pitch about the XDSM paper (no scrolling & discussion, just show the paper and move on)
- [ ] biographical notes (e.g. PhD work) seem out of place as part of the narration.. I think maybe this is similar to the question of showing the presenter, it takes away from the content.. maybe just reference OpenAeroStruct and leave details to a reference slide, video notes, etc.
- [ ] I might have missed it, but the Failure node did not seem to be addressed.. It seems like it's a boolean output of the Structures module or a constraint on the optimizer (and thus left for future discussion?)
- [ ] re: XDSM vs N2... wondered if it would make sense to describe the XDSM as presentation-oriented, and the N2 as debug-oriented?


## Main message
XDSM diagrams are a good tool for visualizing models, understanding solver loops, and specifying interfaces between models developed by more than one person.

## What is an XDSM?
- XDSM stands for extensible design structure matrix
- it came from Lambe and Martins
- it's an standardized extension of a very common DSM idea
- things on the diagonals are computed
- things on the off-diagonals are passed
- it's evolved over time; some people follow a strict coloring scheme, others don't
- some people show just gray for data and others show compute black line

https://link.springer.com/article/10.1007/s00158-012-0763-y
https://github.com/mdolab/pyXDSM
http://websites.umich.edu/~mdolaboratory/pdf/Lambe2012a.pdf
https://github.com/onodip/OpenMDAO-XDSM


## XDSM for analysis
- we can start with the simple cases
- here we focus on showing the different disciplines and how info is passed between them

## XDSM for optimization
- now we basically take an existing analysis XDSM and slap an optimizer around it
- the main difference is that we're showing what variables and functions of interest are being computed
- we also show on the lefthand side which values we care about in the optimal sense

## Making XDSMs
- hey you can just draw them by hand or computer, it's pretty easy to get a rough one
- you **absolutely should** draw an XDSM of the model you're making otherwise it's gonna be so hard to understand what's going on. you can always add to it

## How XDSMs can be used in large projects
- XDSMs are paramount to success for large collaborative projects
- you can put down names of people who are working on specific analysis blocks
- it helps to define the inputs and outputs to each analysis block so individual application developers know what to have as their puzzle piece edges
- another neat thing about XDSMs is using them for automated testing
- once you get to an insanely large model you want to be able to ensure the model matches your XDSM
- NASA Glenn has some code set up to help make this happen
- if the variables being passed around don't match the XDSM then the test throws an error
- this is useful for when models are evolving

## XDSMs in relation to the N2 diagram
- the XDSM is inherently related to the N2 diagram that can be made in OM
- usually the XDSM is higher level than the N2; doesn't show all the variables, only the important ones
- here we'll show an XDSM side by side with an N2 for the same problem
- "the hierarchy gives a much stronger visual of how process-flow should work. The N2 shows how the data connections exist between components" - Justin, 2022
