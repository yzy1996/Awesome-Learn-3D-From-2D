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



Smoothness





## Literature

- [An Intriguing Failing of Convolutional Neural Networks and the CoordConv Solution](https://arxiv.org/abs/1807.03247)  
  **[`NeurIPS 2018`]** *Rosanne Liu, Joel Lehman, Piero Molino, Felipe Petroski Such, Eric Frank, Alex Sergeev, Jason Yosinski* 

- [FiLM: Visual Reasoning with a General Conditioning Layer](https://arxiv.org/abs/1709.07871)  
  **[`AAAI 2018`]** *Ethan Perez, Florian Strub, Harm de Vries, Vincent Dumoulin, Aaron Courville* 

- [End-to-End Learnable Geometric Vision by Backpropagating PnP Optimization](https://arxiv.org/abs/1909.06043)  
  **[`CVPR 2020`]** *Bo Chen, Alvaro Parra, Jiewei Cao, Nan Li, Tat-Jun Chin* 

- [On the Spectral Bias of Neural Networks](https://arxiv.org/abs/1806.08734)  
  **[`ICML 2019`]** *Nasim Rahaman, Aristide Baratin, Devansh Arpit, Felix Draxler, Min Lin, Fred A. Hamprecht, Yoshua Bengio, Aaron Courville* 

- [Implicit Neural Representations with Periodic Activation Functions](https://arxiv.org/abs/2006.09661)  
  **[`NeurIPS 2020`]** *Vincent Sitzmann, Julien N. P. Martel, Alexander W. Bergman, David B. Lindell, Gordon Wetzstein* 

- [Fourier Features Let Networks Learn High Frequency Functions in Low Dimensional Domains](https://arxiv.org/abs/2006.10739)  
  **[`NeurIPS 2020`]** *Matthew Tancik, Pratul P. Srinivasan, Ben Mildenhall, Sara Fridovich-Keil, Nithin Raghavan, Utkarsh Singhal, Ravi Ramamoorthi, Jonathan T. Barron, Ren Ng* 

- [Beyond Periodicity: Towards a Unifying Framework for Activations in Coordinate-MLPs](https://arxiv.org/abs/2111.15135)  
  **[`arXiv 2021`]** *Sameera Ramasinghe, Simon Lucey* 

- [Learning Smooth Neural Functions via Lipschitz Regularization](https://arxiv.org/abs/2202.08345)  
  **[`SIGGRAPH 2022`]** *Hsueh-Ti Derek Liu, Francis Williams, Alec Jacobson, Sanja Fidler, Or Litany* 

- [Neural Implicit Surface Evolution using Differential Equations](https://arxiv.org/abs/2201.09636)  
  **[`arXiv 2022`]** *Tiago Novello, Vinicius da Silva, Guilherme Schardong, Luiz Schirmer, Helio Lopes, Luiz Velho* 

- [Riemannian Score-Based Generative Modelling](https://arxiv.org/abs/2202.02763)  
  **[`arXiv 2022`]** *Valentin De Bortoli, Emile Mathieu, Michael Hutchinson, James Thornton, Yee Whye Teh, Arnaud Doucet* 
