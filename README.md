# scatmod - Open Source Acoustic Scattering Models for fisheries acoustics

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents** 

  - [About](#about)
  - [Types of scattering models --- Start only](#types-of-scattering-models-----start-only)
  - [Which model to use? --- Start only](#which-model-to-use-----start-only)
  - [Multiscattering](#multiscattering)
  - [TO DO:](#to-do)
- [Models in](#models-in)
    - [Analytical](#analytical)
  - [Examples](#examples)
    - [Installing](#installing)
  - [Running the tests](#running-the-tests)
  - [Primary Authors](#primary-authors)
  - [License](#license)
  - [Acknowledgments](#acknowledgments)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


## About
*scatmod* is a platform to distribute and develop acoustic scattering models, with the aim of simulating acoustic targets (e.g. fish, zooplankton, phytoplankton, crustaceans, jellyfish, bubbles, etc.). 

*scatmod* aims to be a cross-language platform, containing models written in various languages, including Matlab, Python and R. 
In order to keep Scatmod consistent, documentation standards have been defined for all used languages.

*scatmod* is developped and maintained by members of the [ICES WGFAST group](https://www.ices.dk/community/groups/Pages/WGFAST.aspx) originating from various institutes including [NWFSC NOAA](https://www.nwfsc.noaa.gov/), [Scripps Institute Of Oceanography](https://scripps.ucsd.edu/), [St Andrews University](https://risweb.st-andrews.ac.uk/portal/en/organisations/school-of-biology(a348f890-b967-4e22-a8ae-75e33143747f).html), [NIWA](https://www.niwa.co.nz/our-science/coasts-and-oceans) and [CMR](https://www.cmr.no/)

## Types of scattering models --- Start only

Three major categories of scattering models can be distinguished:

<hr>


- Analytic / semi-analythic models
  * *Application:* for simple geometric shapes (e.g. spheres, cylinders, prolate spheroids)
  * *Advantages:* exact, fast, not restricted in frequency/material properties
  * *Disadvantages:* not possible to resolve for complex, realistic targets, assumes a single scattering object
  
<p align="center">
<a href="url"><img src="https://github.com/SvenGastauer/scatmod/blob/master/pictures/analytical_illustration.png"  height="150"></a>
</p>

<hr>

- Numerical models
  * *Models:* Finite Element Methods (FEM), Boundary Element Methods (BEM), combinations of those
  * *Application:* Arbitrary shapes, frequencies and materials
  * *Advantages:* 
    - allows for modelling of complex shapes and internal structures
    - includes diffraction / Fluid-Structure-Interaction (FSI) 
    - can be applied to arbitrary materials and frequencies
  * *Disadvantages:* 
    - Computationally complex and expensive

<p align="center">    
<a href="url"><img src="https://github.com/SvenGastauer/scatmod/blob/master/pictures/numeric_illustration.png"  height="150"></a>
</p>

<hr>


- Approximate models
  * *Models:* Kirchhoff Ray Mode (KRM), Distorted Wave Born Approximation(DWBA), Deformed Cylinder Model (DCM), Resonance Scattering, etc.
  * *Application:* Various scattering surface and orientations for a range of frequencies (model dependent)
  * *Advantages:* 
    - Can represent arbitrary scattering surface and orientations
    - (very) fast and relatively simple
  * *Disadvantages:*
    - Frequency restrictions for some models
    - Does not include diffraction effects or internal structure implicitly
    - Multibody scattering generally assumed to be linearly additive
 
<p align="center">
<a href="url"><img src="https://github.com/SvenGastauer/scatmod/blob/master/pictures/approx_illustration.png"  height="150"></a>
</p>

## Which model to use? --- Start only

<hr>


- **Gas bubbles or swimbladders**
 * *Best:* 
    - Numerical models for complex shapes e.g. BEM, FEM
    - Analystical solutions for simple shapes
 * *Easier:*
    - Resonance scattering: Find he resonance frequency, high frequencies for small bubbles, low frequencies for swimbladders
    - KRM: Limited to high frequencies, can be used for flesh and swimbladder if swimbladdered fish are to be modelled
 *Examples:*

<hr>


- **Bones**
 * *Best:* 
    - Numerical models for complex shapes e.g. BEM, FEM
    - Analystical solutions for simple shapes
 * *Easier:*
    - DCM 
 *Examples:*

<hr>

 
- **Fluid-like / flesh**
 * *Best:*
    - Numerical models for complex shapes e.g. BEM, FEM
    - Analystical solutions for simple shapes
 * *Easier:*
    - DCM 
    - DWBA
    - KRM
*Examples:*

## Model Descriptions

**Analytical models**
- [Analytical fluid-like sphere](https://github.com/SvenGastauer/scatmod/blob/master/docs/Analytical_FluidLikeSphere.ipynb)

**DWBA**
- [DWBA](https://github.com/SvenGastauer/scatmod/blob/master/docs/DWBA.ipynb)

## Multiscattering 

-> Put some content here...
The idea is to talk about the different options to model multiscattering, e.g. simple linear addition, the case of bubbles, the more complex cse of reality (mention possible methods and BEM/FEM options)

## TO DO:
- Write documentation standard for R, Python and Matlab
- Define validation standards for new models, e.g. Jupyter/Markdown templates for comparison to analystical model

# Models in

### Analytical
- Sphere and finite cylinde:
  - Solid / rigid
  - Pressure release
  - Elastic
  - Shelled
  
## Examples

### Installing

A step by step series of examples that tell you how to get a development env running

Say what the step will be

```
Give the example
```

And repeat

```
until finished
```

End with an example of getting some data out of the system or using it for a little demo

## Running the tests

Explain how to run the automated tests for this system

## Primary Authors

* **Sven Gastauer** - *blablalbla
* **Dezhang Chu** - *blablalbla
* **Roland Proud** - *blablalbla
* **Yoann Ladroit** - *blablalbla
* **Geir Pedersen** - *blablalbla
* **Pablo Escobar** - *blablalbla

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone whose code was used
* Inspiration
* etc
