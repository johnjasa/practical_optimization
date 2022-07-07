tags: #model_construction #high_priority 

How to construct and use a good surrogate model?
how to check if it's going well
use these for guessing within pycycle


## Main message
Creating high-quality surrogate models is necessary for a lot of MDO. To do this, you need to have a reasonable sampling of the data, understand what a good fit looks like, and know the accuracy and limitations of the surrogate.

## Selecting the right surrogate model and training it
- if your data is regular or irregular, continuous or jumpy, the best model will vary
- think about the amount of training data, dimensionality, if you'll have gradients or not
- when you train it, be mindful of overfitting or underfitting

## How to test your surrogate fit
- use leave one out (LOO) testing
- run the model straight up at different points in the design space
- ensure that you have good fit in the area where you'll be designing