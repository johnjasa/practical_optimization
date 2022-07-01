tags: #differentiation

## Main message
You need to tell OpenMDAO how to compute the total derivatives if you want to do gradient-based optimization. You can do this by specifying partial derivatives, requesting FD on the subsystem level, or using FD on the full system.