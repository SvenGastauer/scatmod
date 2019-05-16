This vignette will provide a brief description of the DWBA model used within the ZooScatR package, explain the needed input parameters and provide a few examples.  

## Quick Start

For a quick start, a minimal example:  

## The DWBA model - a brief explanation
A detailed description of the DWBA model and its application to the scattering properties of zooplankton can be found in  
The DWBA for a body of an arbitrary shape and size for an arbitrary frequency can be written as:
<p align="center"><img src="/docs/tex/dfd12002709fa4d6e6d2034e8cb4e17f.svg?invert_in_darkmode&sanitize=true" align=middle width=248.93387309999997pt height=37.51355025pt/></p>  

or under the simplified form for a deformed cylinder:    
<img src="/docs/tex/0c1baa1b048b249e70f4b958fc914145.svg?invert_in_darkmode&sanitize=true" align=middle width=340.05380969999993pt height=34.544367pt/>
where:  

* <img src="/docs/tex/3599b22805162ca2350153e15581c321.svg?invert_in_darkmode&sanitize=true" align=middle width=20.033194499999986pt height=22.831056599999986pt/> is the scattering amplitude,  
* <img src="/docs/tex/63bb9849783d01d91403bc9a5fea12a2.svg?invert_in_darkmode&sanitize=true" align=middle width=9.075367949999992pt height=22.831056599999986pt/> is the wavenumber defined as <img src="/docs/tex/36b6c63d24db353bb001d01e8135a85f.svg?invert_in_darkmode&sanitize=true" align=middle width=14.652506549999996pt height=27.77565449999998pt/> where <img src="/docs/tex/fd8be73b54f5436a5cd2e73ba9b6bfa9.svg?invert_in_darkmode&sanitize=true" align=middle width=9.58908224999999pt height=22.831056599999986pt/> is the acoustic wavelength [m].  
* <img src="/docs/tex/51f9fb8bcc861c04f7bbdd1ac1f104c0.svg?invert_in_darkmode&sanitize=true" align=middle width=41.17917869999999pt height=30.648287999999997pt/> with freqency <img src="/docs/tex/190083ef7a1625fbc75f243cffb9c96d.svg?invert_in_darkmode&sanitize=true" align=middle width=9.81741584999999pt height=22.831056599999986pt/> in [Hz] and <img src="/docs/tex/3e18a4a28fdee1744e5e3f79d13b9ff6.svg?invert_in_darkmode&sanitize=true" align=middle width=7.11380504999999pt height=14.15524440000002pt/> the soundspeed in the surrounding fluid [m/s]),  
* the subscript <img src="/docs/tex/6f9bad7347b91ceebebd3ad7e6f6f2d1.svg?invert_in_darkmode&sanitize=true" align=middle width=7.7054801999999905pt height=14.15524440000002pt/> refers to the surrounding fluid, the subscribt <img src="/docs/tex/4bdc8d9bcfb35e1c9bfb51fc69687dfc.svg?invert_in_darkmode&sanitize=true" align=middle width=7.054796099999991pt height=22.831056599999986pt/> refers to the scattering body,  
* <img src="/docs/tex/39b09f0f841f556b1bdd88964f27a271.svg?invert_in_darkmode&sanitize=true" align=middle width=26.88577154999999pt height=23.488575000000026pt/> is the position vector along the body axis,  
* <img src="/docs/tex/6c4adbc36120d62b98deef2a20d5d303.svg?invert_in_darkmode&sanitize=true" align=middle width=8.55786029999999pt height=14.15524440000002pt/> in the general model is the integration vloume of the body with the position vector <img src="/docs/tex/39b09f0f841f556b1bdd88964f27a271.svg?invert_in_darkmode&sanitize=true" align=middle width=26.88577154999999pt height=23.488575000000026pt/>  
* <img src="/docs/tex/f9f9c5c673cd3cfbc89d70e50d5566e6.svg?invert_in_darkmode&sanitize=true" align=middle width=15.77667134999999pt height=14.15524440000002pt/> and <img src="/docs/tex/22ef6a467610eca74b917d0b8925099a.svg?invert_in_darkmode&sanitize=true" align=middle width=15.330894149999992pt height=14.15524440000002pt/> are related to the body material properties with <img src="/docs/tex/3cf4fbd05970446973fc3d9fa3fe3c41.svg?invert_in_darkmode&sanitize=true" align=middle width=8.430376349999989pt height=14.15524440000002pt/> - the density contrast and <img src="/docs/tex/2ad9d098b937e46f9f58968551adac57.svg?invert_in_darkmode&sanitize=true" align=middle width=9.47111549999999pt height=22.831056599999986pt/> the soundspeed contrast. Both contrasts are the ratio of the density (<img src="/docs/tex/df3ff70aed72639243c661ee9225263f.svg?invert_in_darkmode&sanitize=true" align=middle width=13.150207949999997pt height=24.575218800000012pt/>) or soundspeed (<img src="/docs/tex/2756c6e77e9e99f16b24e5498afd8387.svg?invert_in_darkmode&sanitize=true" align=middle width=12.204606149999998pt height=23.58895770000001pt/>) inside the body and the surrounding fluid.  
    *  $\gamma_k = \frac{(1 - gh^2)}{gh^2}$ is the compressibility  

    *  $\gamma_{\rho} = \frac{(g - 1)}{g}$  is related to the density contrast  
    

* <img src="/docs/tex/3bf0fa37c82e15ab198d2b9aaf936a76.svg?invert_in_darkmode&sanitize=true" align=middle width=15.667843949999991pt height=22.465723500000017pt/> is a Bessel function of the first kind and first order  
* <img src="/docs/tex/edea2cf7f4395e1257a3a7f719b5a324.svg?invert_in_darkmode&sanitize=true" align=middle width=28.10423384999999pt height=22.831056599999986pt/> is the angle between the incident wave and the target axis.  
  
The equation part inside the shape integral for the DWBA can be split up into three parts:  

* The material properties <img src="/docs/tex/4d9ee86121885fcb1cdff589e33bc8a4.svg?invert_in_darkmode&sanitize=true" align=middle width=52.02067199999999pt height=19.1781018pt/>
* The phase <img src="/docs/tex/06aca0d913f4df2cd1b6dd8c7ddb0355.svg?invert_in_darkmode&sanitize=true" align=middle width=62.96541899999998pt height=34.544367pt/>
* The shape (rest)

## Loading parameters into ZooScatR
  
Before the DWBA model can be run several parameters have to be set.  
Some example configuration files containing all parameters can be found in: `r  paste0(system.file(package="ZooScatR"),"/extdata/configs")`
Parameters (config files) can be loaded into ZooScatR:
## The input parameters  
Based on the previously discussed parts of the equation and the structure of the parameters file, the DWBA takes four different categories of input parameters (shape, orientation, material properties and modelling parameters).  
  
A brief description, the input format, the influence of the parameter and its name within the parameter list are outlined below:  

### Shape parameters  
   
### Orientation parameters:  

  
### Material properties parameters
   
### Simulation parameters  
