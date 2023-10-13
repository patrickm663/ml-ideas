# ML Ideas
This repo serves as a way to gather my thoughts on some algorithms I have been wanting to build and test out. Discussions and PRs welcome!

## Bagging
Bagging (bootstrap aggregation) is a technique where features and observations are sampled (with replacement) and used to train a number of (simple) models to each bootstrap sample. All the models outputs are aggregated to produce a final output. This is a type of ensemble modelling technique.

The most well known model that uses bagging is the random forest algorithm, where shallow decision trees are fit on the bootstrap samples. Either a fixed number of features are sampled or a random number.

I want to test out some extensions to bagging, where we take shallow neural networks (say 2 layers with $\tanh$ activations and some link function) instead of decision trees. I think the neural nets have an advantage for regression tasks because it produces a continuous output.

Furthermore, we can test if adding weightings (standard OLS, regularisation, MCMC) helps avoid overfitting. The models with the n-highest weights (or most accurate) can either be examined further, or taken as a simplified representation of the ensemble model. Feature importance can then be taken by ranking the most accurate models and then ranking the frequency features appeared.

In terms of uncertainty, placing priors in the vector of weights mean we can derive a posterior using MCMC and then produce uncertainty estimates. Or, we could take the output of the model as the mean of some Normal distribution and estimate a posterior for the variance using MCMC.

## Gradient Boosting
TODO, but thinking here about much of the same as above, using shallow neural nets, MCMC methods for the weighting to the model on the residuals. Explainability could be in the form of the last n models being used as a surrogate.

## Neural Nets
For now two main ideas wrt tabular data:

1. Additive decompositions of NNs by isolating features (passing it through the NN in isolation) and applying a weighting to the components. The model can be simplified by dropping features with an absolute weighting below some threshold
2. Finding an heuristic for a trained, deep NN. Conceptually, it is a short-cut to come to a conclusion by finding some simple representation of a deep NN. The error is expected to increase, but short paths (perhaps based on input) may be found in the NN which can make the network simpler to work with and conceptualise. For example, have it output a pipeline of simple transformations which can act as a heuristic under certain conditions.
