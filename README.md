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

### An idea regarding implementing neural nets
A *persistent* data structure is a data structure that supports multiple versions simultaneously.
This is in contrast to an *ephemeral* data structure, that allows only a single version to exist at a time.

Performing an operation on an ephemeral data structure results in the data structure being "used up". Consequently, unless he takes pains to retrieve it, the data structure is unavailable for further use by the programmer. This property has at least two consequences. Firstly, it makes it difficult to implement data structures that have multiple futures e.g. to exploit parallelism, or perform backtracking etc. Secondly, it results in the complication of even simple algorithms.

In object-oriented programming languages like Python, neural networks tend to be implemented as *ephemeral data structures*.
Functional languages, on the other hand, have the property that *all* data structures are persistent by default. (One may still use ephemeral data structures in a functional language when necessary.) I should like to test out a purely functional implementation of a neural network, where we use a persistent rather than an ephemeral data structure.

In addition, I aim to use ideas from category theory. I believe that this will result in an implementation that will clearly distinguish between the structure and meaning of a neural net. This separation will enable both the construction and training of neural networks to be conducted in a compositional fashion.