+++
title = "Microlensing 23"
date = "28 Jan 2019"
type = "page"
hidden = false
weight = 20190128
+++


# [23rd International Microlensing Conference](https://microlensing.science/23/)
28-30 January, 2019

Center for Computational Astrophysics

New York, NY, USA


{{<revealjs theme="psu" transition="slide" controls="true" progress="true" history="false" center="false" loop="false" pdfSeparateFragments="false" showNotes="true" >}}

### Strategies for exploring parameter space for planetary microlensing events:
### Lessons from the RV and TTV community

Eric Ford

Penn State

23rd International Microlensing Conference

Center for Computational Astrophysics

28-30 January, 2019

---

## Challenge:  Multi-modal likelihood

- Multiple local maxima
- Widely spaced
- Separated by deep valleys
- Sharp features
- High-dimensional

___

## Who else has these challenges?

___

## Who else has these challenges?

- Radial velocity
- Astrometry
- Transit search
- Transit timing variations
___
## Similarities

- Non-linear likelihood
- Likelihood highly multi-modal in orbital period
- 5-7 parameters per planet
- Unknown number of planets
- Keplerian orbits

---

## Explore

vs

## Exploit

___

## Explore

1.  Physical intuition
2.  Computational power

___

## Explore:  Physical intution

Full model:  N-body
Surrogate models:
- Keplerian orbits
- Epicycle approximation
- Circular orbits
- Linear/quadratic trajectory?

___

## Explore:  Physical intution

Heirarchy of parameters
- 1-3 key multi-modal parameters
- Secondary non-linear parameters
- (Nearly) linear parameters


___
### Key multi-modal parameters

Brute force search
- Parallelizes efficiently
- GPUs (if high compute per memory load)
___
### Linear (or nearly linear) parameters
- Optimize analytically w/ linear algebra
- Margainlize w/ Laplace approximation

___
### Other non-linear parameters
- Optimize itteratively
- Marginalize via quadrature

___
## Explore:  Physical intution

Heirarchy of parameters
- 1-3 key parameters:
   - Brute force
- Non-linear parameters:
   - Optimize itteratively, or
   - Integration by quadrature
- (Nearly) linear parameters:
   - Optimize analytically, or
   - Integration via Laplace approximation
___

## Example: RV (Keplerian Orbits)

Heirarchy of parameters

- Key parameters:
   - Orbital Period(s)
- Linear parameters:
   - RV amplitiudes (2/planet)
   - Instrumental offsets
- Non-linear parameters:
   - Eccentricities
   - Orbital Phases
   - Noise model
___

## Example: RV (Epicycle Approximation)

Heirarchy of parameters
- Key parameters:
   - Orbital Period(s)
- Linear parameters:
   - RV amplitiudes (4/planet)
   - Instrumental offsets
- Non-linear parameters:
   - Noise model

___

## Example: Transit Photometry

Heirarchy of parameters
- Key parameters:
   - Orbital period
   - Orbital phase
   - Transit duration
- Linear parameters:
   - Transit depth
   - Coefficients for detrending
- Non-linear parameters:
   - Noise model

___
## Example: Transit Photometry

Heirarchy of parameters
- Key parameters:
   - Orbital periods
   - Orbital phases
- Non-linear parameters:
   - Masses
   - Eccentricity vectors
- Insensitive parameters:
   - Inclinations
   - Nodes

___

## Explore:  Physical Intuition

Fast model evaluation
- Density of sampling in period
- 1 Physical model, many viewing geometries
- Small eccenricity approximation

---
## Exploit

What is your goal?

___
## Exploit

- Find optima: Itterative optimizer
- Draw posterior sample (near optimum): MCMC
- Marginalize around optimum: Importance Sampling

___

## Exploit: Optimization

Optimization algorithms using gradients
- Differentiable form of Kepler (Pal 2009)
- Derivatives of Kepler equation by hand
- Autodifferentiation

___
## Exploit: Posterior Sampling

Artisinal MCMC proposals
- Use physically motivated proposals for correlated parameters (Ford 2005)
- Enable jumps between few known modes (Hu+ 2014)
___
## Exploit: Posterior Sampling

Workhorse algorithms
- Ensemble samplers (D~10s)
   - Differential Evolution MCMC (ter Braak 2006; Nelson+ 2013)
   - Affine invariant ensemble sampler (Goodman & Weare 2010)
___
## Exploit: Posterior Sampling

Workhorse algorithms
- Geometric samplers (large D)
   - HMC + No U-Turn Sampler (NUTS; Hoffman & Gelman 2014)
   - Geometric Adaptive Monte Carlo (Tuchow+ 2019)
---

## How many planets?
___
## How many planets?

From Astronomer intuition to Bayesian model comparison
- Requires accurate noise model
- Better to marginalize over noise model parameters than guess wrong
  - "Jitter parameter"
  - Strength of correlated noise
___

## Bayesian Model Comparison
- In general, computationally very expensive
- AIC or BIC are merely heuristics
___
## Bayesian Model Comparison
- Laplace approximation
- Integrated Nested Laplace Approximation (INLA; Rue+ 2009)
- Importance Sampling
   - Mixture of Gaussians (or Student t-distributions)
   - Product of marginals (Perrakis+ 2014)
- Ratio estimator (Nelson+ 2014)
- Diffusive Nested Sampling (DNest4; Brewer & Foreman-Mackey 2018)
- Thermodynamic integration
___
## Extremely Precise RV Evidence Challenge

Lessons learned
- Validate codes
- Do not trust internal errors estimates
- Plan for uncertainty in evidence estimates

___
## Extremely Precise RV Evidence Challenge

Dispersion in evidence estimates
- 0 planets: ~3x
- 1 planet:  ~10x
- 2 planets: 100-1000x
- 3 planets: >10,000x

Nelson+ 2019

---
## What's the real goal?
___
## Characterizing Planet Populations
___
## Heirarchical Bayesian Models

- High-dimensional
- Priors can be surprisingly important

___
## Heirarchical Bayesian Models

- Probabilistic programming languages good for prototyping
   - JAGS
   - STAN
   - Turing.jl
- Incorporating complex survey details can be difficult
   - Approximate Bayesian Computing

---
# Questions?

{{</revealjs>}}
