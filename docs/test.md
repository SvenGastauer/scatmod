---
title: "Running a DWBA simulation programmatically"
author: "Sven Gastauer"
date: "`r Sys.Date()`"
bibliography: vignettes.bib
output:
  rmarkdown::html_vignette:
    toc: true
    toc_depth: 4
vignette: >
  %\VignetteIndexEntry{Running a DWBA simulation programmatically}
  %\VignetteEngine{knitr::rmarkdown}
  %\usepackage[utf8]{inputenc}
---

```{r setup, echo = FALSE, message = FALSE}
knitr::opts_chunk<img src="/docs/tex/29508570159d4ba7b5161abdfdbfad84.svg?invert_in_darkmode&sanitize=true" align=middle width=2060.2971344999996pt height=203.6529759pt/><img src="/docs/tex/b481380cbd3299585c6b491cb6446edd.svg?invert_in_darkmode&sanitize=true" align=middle width=234.33911325pt height=34.544367pt/><img src="/docs/tex/48e387db263e0cd8dc9e4d7d095e5326.svg?invert_in_darkmode&sanitize=true" align=middle width=372.05583359999997pt height=45.84475499999998pt/>f_{bs} = \frac{k_s}{4}\int_{\vec{r_{pos}}}a_c(\gamma_\kappa - \gamma_{\rho})e^{2i\vec{k_b}\vec{r_{pos}}}\frac{J_1(2k_ba_{c}cos\beta_{tilt})}{cos\beta_{tilt}}<img src="/docs/tex/c71a472712fd8e7f0b95af27c62780ce.svg?invert_in_darkmode&sanitize=true" align=middle width=53.995514099999994pt height=39.45205440000001pt/>f_{bs}<img src="/docs/tex/182f2263df391116459fc822e94ebc14.svg?invert_in_darkmode&sanitize=true" align=middle width=200.6641989pt height=22.831056599999986pt/>k<img src="/docs/tex/841b9a457297bbae963323a61322b859.svg?invert_in_darkmode&sanitize=true" align=middle width=203.99652734999998pt height=22.831056599999986pt/>\frac{2\pi}{\lambda}<img src="/docs/tex/1da9fcafafb5c088ab6ddc5e21359621.svg?invert_in_darkmode&sanitize=true" align=middle width=44.86319144999999pt height=22.831056599999986pt/>\lambda<img src="/docs/tex/166108f59748801af4b557a664ee6328.svg?invert_in_darkmode&sanitize=true" align=middle width=216.07983539999995pt height=24.65753399999998pt/>\lambda = \frac{f}{c}<img src="/docs/tex/f6e99773275aaf2ac99ec3c24aab6240.svg?invert_in_darkmode&sanitize=true" align=middle width=99.83792114999999pt height=22.831056599999986pt/>f<img src="/docs/tex/92d230137e6b22d6c02da75e2bb321ca.svg?invert_in_darkmode&sanitize=true" align=middle width=75.14213189999998pt height=24.65753399999998pt/>c<img src="/docs/tex/87d3981f07d7b544c4e52a9a7ea99981.svg?invert_in_darkmode&sanitize=true" align=middle width=427.50031334999994pt height=24.65753399999998pt/>s<img src="/docs/tex/4ad9e89eb727de58aa4a92885dfdacff.svg?invert_in_darkmode&sanitize=true" align=middle width=312.72522434999996pt height=22.831056599999986pt/>b<img src="/docs/tex/90c0d9f7d89edf4faf845c3c3bfd9762.svg?invert_in_darkmode&sanitize=true" align=middle width=208.16387295pt height=22.831056599999986pt/>\vec{r_{pos}}<img src="/docs/tex/e30e882c4ada90e2f241edbf32f81143.svg?invert_in_darkmode&sanitize=true" align=middle width=283.0246088999999pt height=22.831056599999986pt/>v<img src="/docs/tex/77439e78f9400ec2359314faa3286cc2.svg?invert_in_darkmode&sanitize=true" align=middle width=544.6178001pt height=22.831056599999986pt/>\vec{r_{pos}}<img src="/docs/tex/60e0c04e90aac4b310b6faccad06b5ff.svg?invert_in_darkmode&sanitize=true" align=middle width=8.219209349999991pt height=15.296829900000011pt/>\gamma_k<img src="/docs/tex/fd92a53167b3c6ae9574071613d555dc.svg?invert_in_darkmode&sanitize=true" align=middle width=27.11199479999999pt height=22.831056599999986pt/>\gamma_{\rho}<img src="/docs/tex/577c40ffdc0b9f2b596354fac9ed186a.svg?invert_in_darkmode&sanitize=true" align=middle width=317.31618105pt height=22.831056599999986pt/>g<img src="/docs/tex/3f5bcddd498cc5b07fc22e58272bc8f1.svg?invert_in_darkmode&sanitize=true" align=middle width=178.07827949999998pt height=22.831056599999986pt/>h<img src="/docs/tex/abb16496c0b46a169bf7df8e630642b8.svg?invert_in_darkmode&sanitize=true" align=middle width=462.2032767pt height=24.65753399999998pt/>\frac{\rho_b}{\rho_s}<img src="/docs/tex/a868e9003bfeb82d7c2960445c1d6cd6.svg?invert_in_darkmode&sanitize=true" align=middle width=111.97336754999999pt height=24.65753399999998pt/>\frac{c_b}{c_s}<img src="/docs/tex/70d2e2f8bbe04a2f27cc68156e28a62b.svg?invert_in_darkmode&sanitize=true" align=middle width=305.61450314999996pt height=24.65753399999998pt/>\gamma_k = \frac{(1 - gh^2)}{gh^2}$ is the compressibility  

    + $\gamma_{\rho} = \frac{(g - 1)}{g}$  is related to the density contrast  
    

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

###Shape parameters  
   
### Orientation parameters:  

  
### Material properties parameters
   
### Simulation parameters  
