# Find some structure in input data without extra information
# Additional training criteria
- Inputs $x$ are often much easier to obtain than targets $t$
- Earlier layers in a deep network perform general functions, and can be trained on different tasks for which there _is_ data. While the later layers are more task specific.
- Add axxiliary training objectives
	- Easier and allow the optimization to make faster initial progress
	- Force the network to keep more generic features, as a regularization technique
# Auto-encoders
- Reconstruct the input data to learn its structure
- Can create generative models
- Consist of two parts
	- **Encoder:**
		- Compresses the input, useful feature hierarchy for later supervised tasks
	- **Decoder:**
		- Decompresses the input, can be used as a generative model