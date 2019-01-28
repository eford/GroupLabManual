+++
title = "Microlensing 23"
date = "27 Jan 2019"
type = "page"
hidden = true
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

## Where else has these challenges?

___

## Where else has these challenges?

- Radial velocity
- Astrometry
- Transit timing

---

## Similarities

- Non-linear likelihood
- ~5 parameters per planet
- Unknown number of planets
- Each planet follows (nearly) Keplerian orbits

---

## Explore

vs

## Exploit

___

## Explore

- Brute force search over 1-3 key parameters
- Parallelizes very efficiently
___

## Explore

- RV/TTV: Orbital periods 
- Microlensing?  
   + Time of event
   + Linear trajectory

___

## Exploit

- Find optima: Itterative optimizer
- Sample near optima: MCMC
- Marginalize around optima: Importance Sampling

---
### Explore:  Make most of each evaluation

Linear or nearly linear parameters
- Optimize w/ linear algebra
- Margainlize w/ Laplace approximation

___
### Explore:  Make most of each evaluation

Choose parameterization that results in likelihood being nearly linear function of some parameters

___
### Explore: Make most of each evaluation

1 or 2 non-linear parameters
- Optimize itteratively 
- Marginalize via quadrature

---
### Exploit:  



---
# Questions?

{{</revealjs>}}
