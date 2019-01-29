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

## Questions posted

- How to efficiently search a complex (non-Gaussian) multi-variate parameter space?
- How to weight degenerate solutions?
- Efficient computational methods for solving the triple lens equation.


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

Hierarchy of parameters
- 1-3 key multi-modal parameters
- Secondary non-linear parameters
- (Nearly) linear parameters
- Nuisance parameters

___
### Key multi-modal parameters

Brute force search
- Parallelizes efficiently
- GPUs offer >100x speedup (if high compute per memory load)
___
### Linear (or nearly linear) parameters
- Optimize analytically w/ linear algebra
- Marginalize w/ Laplace approximation

___
### Other non-linear parameters
- Optimize itteratively
- Marginalize via quadrature

___
## Explore:  Physical intution

Hierarchy of parameters
- 1-3 key parameters:
   - Brute force
- Non-linear parameters:
   - Optimize itteratively, or
   - Integration by quadrature
- (Nearly) linear parameters:
   - Optimize analytically, or
   - Integration via Laplace approximation
- Nuisance parameters

---

## Example: RV (Keplerian Orbits)

Hierarchy of parameters

- Key parameters:
   - Orbital Period(s)
- Linear parameters:
   - RV amplitiudes (2/planet)
   - Instrumental offsets
- Non-linear parameters:
   - Eccentricities
   - One angle per planet
   - Noise model
___

## Example: RV (Epicycle Approximation)

Hierarchy of parameters
- Key parameters:
   - Orbital Period(s)
- Linear parameters:
   - RV amplitiudes (4/planet)
   - Instrumental offsets
- Non-linear parameters:
   - Noise model

___

## Example: Transit Photometry

Hierarchy of parameters
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
## Example: Transit Timing Variations

Hierarchy of parameters
- Key parameters:
   - Orbital periods
   - Orbital phases
- Non-linear parameters:
   - Masses
   - Eccentricity vectors
- Nuisance parameters:
   - Inclinations
   - Nodes

___

## Explore:  Physical Intuition

Fast model evaluation
- Density of sampling (e.g., in periods)
- One Physical model... many viewing geometries
- Small eccenricity approximation
- Small mutual inclination approximation
-
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
   - Useful when nearly degeneracies
   - Multiple parameterizations for multiple regimes.
- Enable jumps between few known modes (Hu+ 2014)
- Be extra careful to use well-motivated priors
___
## Exploit: Posterior Sampling

Workhorse algorithms
- Ensemble samplers (D ~ 10's)
- Differential Evolution MCMC (ter Braak 2006; Nelson+ 2013)
- Affine invariant ensemble sampler (Goodman & Weare 2010)

Often "good enough" and saves expert from spending time to design artisinal MCMC proposals

___
## Exploit: Posterior Sampling

Workhorse algorithms
- Geometric samplers (large D)
- HMC + No U-Turn Sampler (NUTS; Hoffman & Gelman 2014)
- Geometric Adaptive Monte Carlo (Tuchow+ 2019)
___
## Exploit: Posterior Sampling

Combine:
- Artisinal proposals (e.g., between modes)
- Ensemble samplers (most important parameters)
- Geometric samplers (e.g., nuisance parameters)

___
## Exploit: Posterior Sampling

Weighting of degenerate solutions comes out naturally

Warnings:
- Posterior width depends on measurement uncertainties
- Correlated noise also affects weighting and location of posterior modes

___
## Exploit: Posterior Sampling

Suggestions:
- Report what you measure well (even if it's not what physicists want)
- Particularly important for summmary statistics
- Can avoid some biases
   - e & omega vs e sin(omega) & e cos(omega)
   - Similar for inclinations
---
## How many planets?
___
## How many planets?

From Astronomer intuition to Bayesian model comparison...
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
- Perform sensitivity tests
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
## Hierarchical Bayesian Models

- High-dimensional
- Priors can be surprisingly important

___
## Hierarchical Bayesian Models

- Probabilistic programming languages good for prototyping
   - JAGS (probably too restrictive for microlensing models)
   - STAN (flexible, heavily templatized C++)
   - Turing.jl (flexible, easier to implement thanks to Julia)

___
## Hierarchical Bayesian Models

- Survey may be homogeneous
- Astrophysical complexity

___
## Hierarchical Bayesian Models

- Incorporating complex survey details can be difficult
- Approximate Bayesian Computing
   - Allows for complex physics, survey practicalities
   - Can gradually build model complexity
   - Enables testingn sensitivity to unmodeled complexities

---
## Towards Reproducibile Science

___
## Towards Reproducibile Science
- Report what you measure well
- Report more than summary statistics
- If degeneracies, report mixture model as approximation to posterior

___
## Towards Reproducibile Science
- Share posterior distributions
- Ideally labeled with log prior & log likelihood (perhaps multiple terms)
- Plan for both data & codes to be shared
___
## Towards Reproducibile Science

Experimental design matters
- Simulations should inform key decissions
- Use algorithmic observing strategies (most of the time)
- Document decisions (esp. deviations)

---
# Questions?

{{</revealjs>}}
