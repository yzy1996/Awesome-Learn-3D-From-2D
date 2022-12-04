# Some tools/tricks

**Issue**:

standard ReLU MLPs fail to adequately represent fine details in these complex low-dimensional signals due to a spectral bias

**Solution**:

- replace the ReLU activations with sine functions
- lift the input coordinates into a Fourier feature space 



[FiLM: Visual Reasoning with a General Conditioning Layer](https://arxiv.org/pdf/1709.07871.pdf)

[AAAI 2018]

Ethan Perez, Florian Strub, Harm de Vries, Vincent Dumoulin, Aaron Courville





Fourier Features Let Networks LearnHigh Frequency Functions in Low Dimensional Domains

Implicit neural representations with periodic activation functions

SIREN replaced the popular ReLU activation function withsine functions with modulated frequencies, showing greatsingle scene fitting results.







The major drawback of training coordinate-MLPs with raw input coordinates is their sub-optimal performance in learning high-frequency content. 

**As a remedy**, recent studies empirically confirmed that projecting the coordinates to a higher dimensional space using sine and cosine functions of different frequencies allows coordinate-MLPs to learn high-frequency information **more effectively**.

Fourier features let networks learn high frequency functions in low dimensional domains



spatial coordinate information is insufficient for the network to learn a continuous 3D representation with limited input.

what we can do is to enrich the representation of each coordinate and compensate for the missing information when only sparse views are provided. It’s pritical to overcome this drawback by 



An intriguing failing of convolutional neural networks and the coordconv solution
