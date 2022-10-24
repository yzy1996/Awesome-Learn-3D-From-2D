# Siren

Implicit Neural Representations with Periodic Activation Functions

NIPS202

Vincent Sitzmann, Julien N. P. Martel, Alexander W. Bergman, David B. Lindell, Gordon Wetzstein





**SIRENS leverage MLPs with periodic activation functions for implicit neural representations.**

better than ReLU-MLPs and positional encoding strategies

#My note#

问题描述

$$
F(\mathbf{x}, \Phi, \nabla_{\mathbf{x}}\Phi, \nabla_{\mathbf{x}}^2\Phi, \dots) =0
$$



representation: 

- continuous parameterization
- discrete grid-based 



相关研究

Fourier neural networks









belong to inverse 

## Deferential Equations (DEs)





siren is compared to ReLU-based mothods

> ReLU networks are piecewise linesr, their second derivative is zero everywhere. They are incapable of modeling information contained in higher-order derivatives of natural signals.

alternative activations, such as tanh or softplus, are capable of representing higher-order derivatives, their derivatives are often not well behaved







They propose to use the sine as periodic activation function:
$$
\Phi(\mathbf{x})=\mathbf{W}_{n}\left(\phi_{n-1} \circ \phi_{n-2} \circ \ldots \circ \phi_{0}\right)(\mathbf{x})+\mathbf{b}_{n}, \quad \mathbf{x}_{i} \mapsto \phi_{i}\left(\mathbf{x}_{i}\right)=\sin \left(\mathbf{W}_{i} \mathbf{x}_{i}+\mathbf{b}_{i}\right)
$$
where 
