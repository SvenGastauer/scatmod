# scatmod
Acoustic Scattering Models
Scatmod is a platform to distribute and develop acoustic scattering models, with the aim of simulating acoustic targets (e.g. fish, zooplankton, phytoplankton, crustaceans, jellyfish, bubbles, etc.). 
Scatmod aims to be a cross-language platform, containing models written in various languages, including Matlab, Python and R. 
In order to keep Scatmod consistent, documentation standards have been defined for all used languages.

## Types of scattering models

Three major categories of scattering models can be distinguished:
- Analytic / semi-analythic models
  * *Application:* for simple geometric shapes (e.g. spheres, cylinders, prolate spheroids)
  * *Advantages:* exact, fast, not restricted in frequency/material properties
  * *Disadvantages:* not possible to resolve for complex, realistic targets, assumes a single scattering object
  
<p align="center">
<a href="url"><img src="https://github.com/SvenGastauer/scatmod/blob/master/pictures/analytical_illustration.png"  height="150"></a>
</p>

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


## Available models and when to use/not to use them:



## TO DO:
- Write documentation standard for R, Python and Matlab
- Define validation standards for new models, e.g. Jupyter/Markdown templates for comparison to analystical model
Models to be included:

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
