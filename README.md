# scatmod - Open Source Acoustic Scattering Models for fisheries acoustics

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents** 

- [About](#about)
- [Types of scattering models --- Start only](#types-of-scattering-models-----start-only)
- [Which model to use? --- Start only](#which-model-to-use-----start-only)
- [Model Descriptions](#model-descriptions)
- [Multiscattering](#multiscattering)
- [TO DO:](#to-do)
- [Models in scatmod](#models-in-scatmod)
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

## Types of scattering models

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

## Which model to use?

<hr>

### Overview Table  

Modified from Jech et al. (2015)

| Model       | Accuracy / Type           | Range of Validity  | Limitations  | Examples  |
|---|---|---|---|---|
| MSS | Exact / Analytical | Canonical shapes (currently 11 available) | Convergence issues with some shapes  | Anderson (1950)      |
| BEM | Quasi-exact / Numerical | All shapes, all frequencies, all angles | High computational demands (slightly better with Fast-Multipole BEM) | Francis et al. (1998); Francis and Foote (2003);  Okumura et al. (2003)|
| FEM | Quasi-exact / Numerical | All shapes, all frequencies, all angles | High computational demands | Zampolli et al. (2007); Macaulay et al. (2013)|
| FMM | Exact / Analytical      | If Axisymmetric - All shapes, all frequencies, all angles  | Non-axisymmetric, convergence issues at high aspect ratios| Reeder and Stanton (2004)|
| KA | Approximate| High Frequencies only, near normal incidence, homogenous material| Off-normal incidence, low frequencies, no circumferential waves| Macaulay et al. (2013)|
| KRM | Approximate| All frequencies, homogenous material; at high frequencies: high aspect ratios; at low frequencies: near-normal incidence |  Off-normal incidence, no circumferential waves, no longitudinal modes of vibration near resonance| Horne et al. (2000); Macaulay et al. (2013); Gastauer et al. (2016)|
| Modal series based DCM| Approximate| Near normal incidence; all frequencies; circular cross-sections; all material | off-normal incidence, low aspect ratios, irregular shapes with high local slopes| Gorska and Ona (2003); Stanton (1989) |
| DWBA (incl PT-DWBA,SDWBA) | Approximate| Weak scatterers (g and h < 1.005 i.e. < 5%), all shapes, all angles | Strong scatterers (g and h > 5%)|Chu and Ye (1999); Demer et al. (2003); Calise and Skaret (2011); Gastauer et al. (2019)  |

#### Model Acoronyms:
- MSS - Exact Modal Series Solutions  
- BEM - Boundary Element Model  
- FEM - Finite Element Model  
- FMM - Fourier Matching Method  
- KA - Kirchhoff Approximation  
- DCM - Deformed Cylinder scattering Model


#### References:
-  *Anderson, V. C. (1950). Sound scattering from a fluid sphere. The Journal of the Acoustical Society of America, 22(4), 426-431.*  
-  *Calise, L., and Skaret, G. (2011). “Sensitivity investigation of the SDWBA Antarctic krill target strength model to fatness, material contrasts and orientation,” Ccamlr Science 18, 97–122.*
-  *Chu, D., and Ye, Z. (1999). “A phase-compensated distorted wave born approximation representation of the bistatic scattering by weakly scattering objects: Application to zooplankton,” J. Acoust. Soc. Am.106, 1732–1743.*  
-  *Demer, D. A., and Conti, S. G. (2003). “Reconciling theoretical versus empirical target strengths of krill: Effects of phase variability on the distorted-wave Born approximation,” ICES J. Mar. Sci. 60, 429–434.*  
-  *Francis, D. T., Foote, K. G., Alippi, A., & Cannelli, G. B. (1998). ‘Boundary-element-model predictions of acoustic scattering by swimbladder-bearing fish. In Proceedings of the Fourth European Conference on Underwater Acoustics (Vol. 1, pp. 255-260). Rome: CNR-IDAC.*  
-  *Francis, D. T., & Foote, K. G. (2003). Depth-dependent target strengths of gadoids by the boundary-element method. The Journal of the Acoustical Society of America, 114(6), 3136-3146.*  
-  *Gastauer, S., Chu, D., & Cox, M. J. (2019). ZooScatR—An r package for modelling the scattering properties of weak scattering targets using the distorted wave Born approximation. The Journal of the Acoustical Society of America, 145(1), EL102-EL108.*  
-  *Gastauer, S., Scoulding, B., Fässler, S. M., Benden, D. P., & Parsons, M. (2016). Target strength estimates of red emperor (Lutjanus sebae) with Bayesian parameter calibration. Aquatic Living Resources, 29(3), 301.*  
-  *Gorska, N., & Ona, E. (2003). Modelling the acoustic effect of swimbladder compression in herring. ICES Journal of Marine Science, 60(3), 548-554.*  
-  *Horne, J. K., Walline, P. D., & Jech, J. M. (2000). Comparing acoustic model predictions to in situ backscatter measurements of fish with dual‐chambered swimbladders. Journal of fish Biology, 57(5), 1105-1121.*  
-  *Jech, J. M., Horne, J. K., Chu, D., Demer, D. A., Francis, D. T., Gorska, N., ... & Reeder, D. B. (2015). Comparisons among ten models of acoustic backscattering used in aquatic ecosystem research. The Journal of the Acoustical Society of America, 138(6), 3742-3764.*  
-  *Macaulay, G. J., Peña, H., Fässler, S. M., Pedersen, G., & Ona, E. (2013). Accuracy of the Kirchhoff-approximation and Kirchhoff-ray-mode fish swimbladder acoustic scattering models. PloS one, 8(5), e64055.*  
-  *Okumura, T., Masuya, T., Takao, Y., & Sawada, K. (2003). Acoustic scattering by an arbitrarily shaped body: An application of the boundary-element method. ICES Journal of Marine Science, 60(3), 563-570.*  
-   *Reeder, D. B., & Stanton, T. K. (2004). Acoustic scattering by axisymmetric finite-length bodies: An extension of a two-dimensional conformal mapping method. The Journal of the Acoustical Society of America, 116(2), 729-746.*  
-  *Stanton T.K. Sound scattering by cylinders of finite length. III. Deformed cylinders, Journal of the Acoustical Society of America, 1989, vol. 86 (pg. 691-705)*  
-  *Zampolli, M., Tesei, A., Jensen, F. B., Malm, N., & Blottman III, J. B. (2007). A computationally efficient finite element model with perfectly matched layers applied to scattering from axially symmetric objects. The Journal of the Acoustical Society of America, 122(3), 1472-1485.*  

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

## Models in scatmod

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

* **Sven Gastauer** - *Antarctic Climate and Ecosystem Cooperative Research Centre, University of Tasmania, Private Bag 80, Hobart, Tasmania 7001, Australia*
* **Dezhang Chu** - *Northwest Fisheries Science Center, National Marine Fisheries Service, National Oceanic and Atmospheric Administration, 2725 Montlake Boulevard East, Seattle, Washington 98112, USA*
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
