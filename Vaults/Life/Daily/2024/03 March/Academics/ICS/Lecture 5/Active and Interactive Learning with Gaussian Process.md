# Active Learning with Gaussian Process Regression
- Spacial case of [[Incremental Learning]]
	- The learning algorithm can interactively query a human user or some other information source, to label new data points with the desired outputs.
- Make predictions on many points in the workspace, and only label the locations where the predictions are the most uncertain.
	- Also the principle behind how [[Bayesian Optimization]] works.

## Incremental aggregation of datapoints (post-MLL maximization)
- If there is enough data to infer the hyperparameters of the kernel, then only the update of the covariance matrix has to be performed when aggregating more data to the model. The hyperparameters are kept fixed.
- A least square update can be performed to avoid recomputing the inverse of the covariance matrix.
- The smart update of the (inverse of the) covariance matrix allows to aggregate data to make a confident prediction the next that point is visited.
	- This can be skipped if the uncertainty of the prediction is already small enough.
