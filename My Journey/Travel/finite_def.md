---
layout: page
title: Finite Deformation Kinematics
---

Let us assume that we have access to data (at quadrature points)
that includes:
- $$\sigma(t)$$: the current Cauchy stress
- $$q^*$$: state variables relevant to material state

As well as a constitutive model that provides a function

## Review: Small Deformation Stress Update Procedure

For the case of small deformation, the update procedure
is pretty straightforward, and the steps go something like this:

> Given:
> - the current stress state, $$\mathbf{\sigma}(t)$$
> - a trial displacement increment, $$\hat{u}$$
>
> 1. Compute the increment in the small strain tensor increment  
> $$ \hat{\varepsilon} = \frac{1}{2}(\nabla \hat{u} + (\nabla \hat{u})^\top) $$
>
> 2. Pass $$\hat{\varepsilon}$$ to the constitutive to update stress  
> $$ \sigma_{new} = \sigma(\sigma_{old}, \hat{\varepsilon}) $$

The function $$\sigma(\cdot, \cdot)$$ may be as simple as 
linear elasticity, or it might be more complicated to account 
for plasticity, hardening/softening, or damage effects. Regardless,
if the displacements are small, 
