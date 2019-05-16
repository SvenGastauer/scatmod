This vignette will provide a brief description of the DWBA model used within the ZooScatR package, explain the needed input parameters and provide a few examples.  

## Quick Start

For a quick start, a minimal example:  

## The DWBA model - a brief explanation
A detailed description of the DWBA model and its application to the scattering properties of zooplankton can be found in  
The DWBA for a body of an arbitrary shape and size for an arbitrary frequency can be written as:
$$
f_{bs} = \frac{k_s}{4}\int\int\int_v(\gamma_k - \gamma_{\rho})e^{2i\vec{k_b}\vec{r_v}}dv
$$  

or under the simplified form for a deformed cylinder:    
$f_{bs} = \frac{k_s}{4}\int_{\vec{r_{pos}}}a_c(\gamma_\kappa - \gamma_{\rho})e^{2i\vec{k_b}\vec{r_{pos}}}\frac{J_1(2k_ba_{c}cos\beta_{tilt})}{cos\beta_{tilt}}$
where:  

* $f_{bs}$ is the scattering amplitude,  
* $k$ is the wavenumber defined as $\frac{2\pi}{\lambda}$ where $\lambda$ is the acoustic wavelength [m].  
* $\lambda = \frac{f}{c}$ with freqency $f$ in [Hz] and $c$ the soundspeed in the surrounding fluid [m/s]),  
* the subscript $s$ refers to the surrounding fluid, the subscribt $b$ refers to the scattering body,  
* $\vec{r_{pos}}$ is the position vector along the body axis,  
* $v$ in the general model is the integration vloume of the body with the position vector $\vec{r_{pos}}$  
* $\gamma_k$ and $\gamma_{\rho}$ are related to the body material properties with $g$ - the density contrast and $h$ the soundspeed contrast. Both contrasts are the ratio of the density ($\frac{\rho_b}{\rho_s}$) or soundspeed ($\frac{c_b}{c_s}$) inside the body and the surrounding fluid.  
    + $\gamma_k = \frac{(1 - gh^2)}{gh^2}$ is the compressibility  

    + $\gamma_{\rho} = \frac{(g - 1)}{g}$  is related to the density contrast  
    

* $J_1$ is a Bessel function of the first kind and first order  
* $\beta_{tilt}$ is the angle between the incident wave and the target axis.  
  
The equation part inside the shape integral for the DWBA can be split up into three parts:  

* The material properties $\gamma_k - \gamma_{\rho}$
* The phase $e^{2i\vec{k_b}\vec{r_v}}dv$
* The shape (rest)

## Loading parameters into ZooScatR
  
Before the DWBA model can be run several parameters have to be set.  
Some example configuration files containing all parameters can be found in: `r  paste0(system.file(package="ZooScatR"),"/extdata/configs")`
Parameters (config files) can be loaded into ZooScatR:
## The input parameters  
Based on the previously discussed parts of the equation and the structure of the parameters file, the DWBA takes four different categories of input parameters (shape, orientation, material properties and modelling parameters).  
  
A brief description, the input format, the influence of the parameter and its name within the parameter list are outlined below:  

###Shape parameters  
   
### Orientation parameters:  

  
### Material properties parameters
   
### Simulation parameters  
