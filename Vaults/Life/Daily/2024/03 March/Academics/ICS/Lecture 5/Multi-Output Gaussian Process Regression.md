# MIMO Gaussian Process
- When dealing with multiple outputs, each one can be modeled as an independent Gaussian Process with different kernel functions and hyperparameters.
	- Fir a Gaussain Process model for each output.
	- Very computationally and memory inefficient.
- Share kernel functions when different outputs can be considered as asmpled from the same generative process.

## Sharing horizontal lengthscales
- Given that the smoothness of the motion can be independent o the cartesian direction, in the case of modeling velocity.

## Sharing output lengthscales
- Must be careful
- Outputs might have different units or different level of energy, so it would not make sense to share their lengthscales.

## Sharing likelihood noise
- Cannot be done if the noise level of the sensors differ a lot.
	- Would make the uncertainty to be miss-calibrated.
- When going into unexplored regions of the workspace, having well-calibrated uncertainty can make a huge difference between a usable and unusable uncertainty prediction.

## Sharing the inducing inputs
- Having different inducing inputs for each output can be intractable when fitting a sparse model.
- Sharing the inducing points among the different outputs can speed up the fitting process and does not have many disadvantages.