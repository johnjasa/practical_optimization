tags: #model_construction 

- discuss what convergence looks like in the terminal
- this is different than optimization convergence
- show examples of it looking great and looking bad
	- three iterations like some wind turbines
	- 40 iterations like the circuit example
	- stalling out on pycycle ([[How to debug solvers]])
	- maybe a relaxed solver vs a non-relaxed one
- explain when atol and rtol matter; it's sort of up to you
- solver needs to converge more than the optimizer tolerance
- discuss the nested tolerance idea (from Eliot's paper)
- 