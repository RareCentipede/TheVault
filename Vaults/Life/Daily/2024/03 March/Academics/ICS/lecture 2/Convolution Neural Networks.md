To process grid-like information like images.

# Weight sharing: spatial equivariance
- Share pieces of network
- Copy the part of the network across the input space, enforce that the weights remain equal.

# Convolution
- Instead of copying parts of the network, slide a part of the network over the input
- Convolution: $$S(i, j) = (I * K)(i, j) = \Sigma_m \Sigma_n I(m, n)K(i - m, j - n)$$
- Detect non-linearities on top of the feature map.
- Optional pooling: take some function over the area of the kernel.