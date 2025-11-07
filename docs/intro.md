
## Foundations of MDE

MDE leverages the [Generalized Embedding Theorem](https://doi.org/10.1371%2Fjournal.pone.0018295) employing [Empirical Dynamic Modeling](https://en.wikipedia.org/wiki/Empirical_dynamic_modeling) to evaluate dynamical manifolds. The generalized embedding theorem is a generalization of Taken's theorem from time-delays to multivariate observations. 

### Time Series as Observations of a Dynamic System
Dynamic systems are both state and time dependent. Here one can see the direct connection between state and time dependence. 
<iframe width="100%" height="335"
src="https://www.youtube.com/embed/fevurdpiRYg"
frameborder="0" allow="autoplay; gyroscope; 
picture-in-picture" allowfullscreen></iframe>

### Takens Theorem
[Takens theorem](https://en.wikipedia.org/wiki/Takens%27s_theorem) 
is a remarkable mathematical result that allows one to reconstruct a
representation of the system dynamics (state-space manifold) from a
single (univariate, 1-D) timeseries observed from the system.  The embedding
results in generation of a higher-dimensional representation of the system.

<iframe width="100%" height="335"
src="https://www.youtube.com/embed/QQwtrWBwxQg" 
frameborder="0" allow="autoplay; gyroscope; 
picture-in-picture" allowfullscreen></iframe>

------

### MDE Generalized Embedding

MDE leverages the generalized embedding theorem to discover optimally informative multidimensional manifolds for a target observable of a multivariate complex saystem. Specifically, given a target observable, scan all other observables to find the best 1-D predictor of the target, ensuring the predictor has causal inference with the target. With this 1-D vector scan all remaining observables to find the 2-D embedding with best predictability and causal inference. This greedy algorithm is iterated up to the point that no further prediction skill improvement can be produced. 
