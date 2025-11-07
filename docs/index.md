## Manifold Dimensional Expansion (MDE)

Manifold dimensional expansion is a causal discovery and dimensionality reduction technique designed to identify low dimensional maximally predictive _observables_ of a multivariate dynamical system. In contrast to many machine learning and statistical representations the discovered variables are _not_ latent, abstract representations of complex system components, but _observables_. 

The algorithm is based on a greedy implementation of the generalized Takens embedding theorem. However, instead of using time delays for dimensionality expansion, _observables_ that improve forecast skill of a target variable are added until no further improvement can be achieved. The default predictor is the  [Empirical Dynamic Modeling (EDM)](https://en.wikipedia.org/wiki/Empirical_dynamic_modeling) [simplex](https://www.nature.com/articles/344734a0) function providing a fully nonlinear predictor.

Causal inference is performed with [Convergent Cross Mapping](https://en.wikipedia.org/wiki/Convergent_cross_mapping) ([CCM](https://science.sciencemag.org/content/338/6106/496)) ensuring the added observable is part of the same dynamical system as the target time series. 

Output is a DataFrame of observation vectors defining a low-dimensional manifold with optimal predictability for the target variable. 
