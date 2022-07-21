tags: #intro

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

## Main message
Tests are so important. You should have tests for your code. Make them for components, groups, small pieces of code, big pieces of code, everything. Write them as soon as possible -- don't put them off.

## What do we mean by tests?
- you want to be able to write code and ensure that it does what you want
- there are two broad categories of tests, unit tests and regression tests
- unit tests work on cute little portions of code and make sure they do what you expect
- regression tests make sure that the code does tomorrow what it did today and yesterday. can include more than just a little section

## How to write a good unit test
- in some cases it might be pretty easy
- Python and OM have a great suite of tools to help you do this
- want to really break it down and look at the smallest reasonable unit
- these should allow to pinpoint where a bug or otherwise was implemented
- you need to test edge cases because otherwise the optimizer will find them

## How to write a good regression test
- gotta establish a baseline
- the best way is to use something from a [[Verification and validation]] basis
- these might be more expensive so you can't always run them every time
- be purposeful about what is a regression test in terms of breadth and depth


## Advanced testing ideas
- XDSM and model matching https://github.com/OpenMDAO/GASPy/blob/dd93647e260fa368d5be058b9d08bb475204640e/GASPy/subsystems/weight_subsystem/wght_subroutine/test/test_fuel_weight.py#L477
- nightly regression tests and tracking times etc