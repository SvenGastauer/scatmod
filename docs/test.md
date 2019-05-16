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
knitr::opts_chunk<img src="/docs/tex/3edcd1ced12fc6e22f39e33825afd6ed.svg?invert_in_darkmode&sanitize=true" align=middle width=2060.2971344999996pt height=166.0273989pt/>rplot #Show the result plot
#Target strength vs angular position
para<img src="/docs/tex/39e451ea59bcd04572867fa6085f35e8.svg?invert_in_darkmode&sanitize=true" align=middle width=37.21207874999999pt height=21.68300969999999pt/>var_indx <- 2 #Set output variable to Angular position
#Run DWBA based on config file
res <- bscat(para=para, misc=misc)
res<img src="/docs/tex/4d97d2af1f04af17ce47d052eebcf4b8.svg?invert_in_darkmode&sanitize=true" align=middle width=587.6747481pt height=24.65753399999998pt/>simu<img src="/docs/tex/17c2dfef76a7e0886931a7a4e2561012.svg?invert_in_darkmode&sanitize=true" align=middle width=405.38304839999995pt height=22.831056599999986pt/>simu<img src="/docs/tex/7d923245fa7432219e1ab3306deb6424.svg?invert_in_darkmode&sanitize=true" align=middle width=700.2747476999999pt height=47.671232400000015pt/>rplot #Show the result plot
#Reduced Target Strength vs Frequency (Wavenumber x width)
para<img src="/docs/tex/39e451ea59bcd04572867fa6085f35e8.svg?invert_in_darkmode&sanitize=true" align=middle width=37.21207874999999pt height=21.68300969999999pt/>out_indx <- 4 #Set output to Reduced Target Strength
para<img src="/docs/tex/39e451ea59bcd04572867fa6085f35e8.svg?invert_in_darkmode&sanitize=true" align=middle width=37.21207874999999pt height=21.68300969999999pt/>var_indx <- 1 #Set output variable to Frequency
#Run DWBA based on config file
res <- bscat(para=para, misc=misc)
res<img src="/docs/tex/cb7ea6d018819fe2b5aa850124a72e4c.svg?invert_in_darkmode&sanitize=true" align=middle width=701.5530620999999pt height=124.74886710000001pt/><img src="/docs/tex/727c37deb763bc9f1f45493e15e7973a.svg?invert_in_darkmode&sanitize=true" align=middle width=234.33911325pt height=34.544367pt/><img src="/docs/tex/48e387db263e0cd8dc9e4d7d095e5326.svg?invert_in_darkmode&sanitize=true" align=middle width=372.05583359999997pt height=45.84475499999998pt/><img src="/docs/tex/d341acc379ba0eb9463d76cfb70810b7.svg?invert_in_darkmode&sanitize=true" align=middle width=340.05380969999993pt height=34.544367pt/><img src="/docs/tex/c71a472712fd8e7f0b95af27c62780ce.svg?invert_in_darkmode&sanitize=true" align=middle width=53.995514099999994pt height=39.45205440000001pt/>f_{bs}<img src="/docs/tex/182f2263df391116459fc822e94ebc14.svg?invert_in_darkmode&sanitize=true" align=middle width=200.6641989pt height=22.831056599999986pt/>k<img src="/docs/tex/841b9a457297bbae963323a61322b859.svg?invert_in_darkmode&sanitize=true" align=middle width=203.99652734999998pt height=22.831056599999986pt/>\frac{2\pi}{\lambda}<img src="/docs/tex/1da9fcafafb5c088ab6ddc5e21359621.svg?invert_in_darkmode&sanitize=true" align=middle width=44.86319144999999pt height=22.831056599999986pt/>\lambda<img src="/docs/tex/166108f59748801af4b557a664ee6328.svg?invert_in_darkmode&sanitize=true" align=middle width=216.07983539999995pt height=24.65753399999998pt/>\lambda = \frac{f}{c}<img src="/docs/tex/f6e99773275aaf2ac99ec3c24aab6240.svg?invert_in_darkmode&sanitize=true" align=middle width=99.83792114999999pt height=22.831056599999986pt/>f<img src="/docs/tex/92d230137e6b22d6c02da75e2bb321ca.svg?invert_in_darkmode&sanitize=true" align=middle width=75.14213189999998pt height=24.65753399999998pt/>c<img src="/docs/tex/87d3981f07d7b544c4e52a9a7ea99981.svg?invert_in_darkmode&sanitize=true" align=middle width=427.50031334999994pt height=24.65753399999998pt/>s<img src="/docs/tex/4ad9e89eb727de58aa4a92885dfdacff.svg?invert_in_darkmode&sanitize=true" align=middle width=312.72522434999996pt height=22.831056599999986pt/>b<img src="/docs/tex/90c0d9f7d89edf4faf845c3c3bfd9762.svg?invert_in_darkmode&sanitize=true" align=middle width=208.16387295pt height=22.831056599999986pt/>\vec{r_{pos}}<img src="/docs/tex/e30e882c4ada90e2f241edbf32f81143.svg?invert_in_darkmode&sanitize=true" align=middle width=283.0246088999999pt height=22.831056599999986pt/>v<img src="/docs/tex/77439e78f9400ec2359314faa3286cc2.svg?invert_in_darkmode&sanitize=true" align=middle width=544.6178001pt height=22.831056599999986pt/>\vec{r_{pos}}<img src="/docs/tex/60e0c04e90aac4b310b6faccad06b5ff.svg?invert_in_darkmode&sanitize=true" align=middle width=8.219209349999991pt height=15.296829900000011pt/>\gamma_k<img src="/docs/tex/fd92a53167b3c6ae9574071613d555dc.svg?invert_in_darkmode&sanitize=true" align=middle width=27.11199479999999pt height=22.831056599999986pt/>\gamma_{\rho}<img src="/docs/tex/577c40ffdc0b9f2b596354fac9ed186a.svg?invert_in_darkmode&sanitize=true" align=middle width=317.31618105pt height=22.831056599999986pt/>g<img src="/docs/tex/3f5bcddd498cc5b07fc22e58272bc8f1.svg?invert_in_darkmode&sanitize=true" align=middle width=178.07827949999998pt height=22.831056599999986pt/>h<img src="/docs/tex/abb16496c0b46a169bf7df8e630642b8.svg?invert_in_darkmode&sanitize=true" align=middle width=462.2032767pt height=24.65753399999998pt/>\frac{\rho_b}{\rho_s}<img src="/docs/tex/a868e9003bfeb82d7c2960445c1d6cd6.svg?invert_in_darkmode&sanitize=true" align=middle width=111.97336754999999pt height=24.65753399999998pt/>\frac{c_b}{c_s}<img src="/docs/tex/70d2e2f8bbe04a2f27cc68156e28a62b.svg?invert_in_darkmode&sanitize=true" align=middle width=305.61450314999996pt height=24.65753399999998pt/>\gamma_k = \frac{(1 - gh^2)}{gh^2}$ is the compressibility  

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
```{r}
# filenmae of an example configuration
fname <- paste0(system.file(package="ZooScatR"),"/extdata/configs/config_0.dat")
#Read the parameter file
para <- read_para(fname)
```
  
the read_para function will load the model parameters as a list of 5:  

* ...<img src="/docs/tex/f9c2c014c7b33022d3db37b2dbb8d19c.svg?invert_in_darkmode&sanitize=true" align=middle width=625.8702317999999pt height=24.65753399999998pt/>shape - Contains all the shape parameters  
* ...<img src="/docs/tex/6967422150cdbfb44cfbdd80539911be.svg?invert_in_darkmode&sanitize=true" align=middle width=353.82040979999994pt height=22.831056599999986pt/>phy - Contains the material properties  
* ...<img src="/docs/tex/c0b4dc992148609177ea39174919209e.svg?invert_in_darkmode&sanitize=true" align=middle width=701.5530653999999pt height=1112.8767143999999pt/>L",
                             "...shape$rho_L",
                             "...shape$L_a",
                             "...shape$order",
                             "",
                             "...shape$Lstd",
                             "...shape$dL",
                             "...shape$prof_name",
                             "...shape$taper_sm",
                             "...shape$axis_sm")
                         ))
knitr::kable(para.df)
```  
   
### Orientation parameters:  

```{r echo=FALSE} 

orient.df <- as.data.frame(cbind(Variable = c("Mean Theta (θ)",
                                      "Orientation Average",
                                      "Theta Distribution (dθ)",
                                      "Min. Theta (θmin)",
                                      "Max. Theta (θmax)",
                                      "Std.(θ)",
                                      "Increment θ"),
                         Unit = c("°",
                                  "Boolean",
                                  "distribution (Uniform or Gaussian)",
                                  "°",
                                  "°",
                                  "°",
                                  "°"),
                         Description = c("Mean orientation angle",
                                         "Defines if an orientation average should be considered",
                                         "PDF of theta",
                                         "Minimum theta for a uniform PDF",
                                         
                                         "Maximum theta for a uniform PDF",
                                         "Standard deviation of theta for a Gaussian PDF",
                                         "Incremental step of theta for a Gaussian PDF"),
                         Influence = c("",
                                       "",
                                       "1) Uniform; 2) Gaussian","","","",""),
                         "Parameters name" =
                           c("...orient$angm",
                             "...orient$ave_flag",
                             "...orient$PDF",
                             "...orient$ang0",
                             "...orient$ang1",
                             "...orient$PDF_para",
                             "...orient$dang")
                         ))
knitr::kable(orient.df, keep.line.breaks = TRUE, style = 'grid', justify = 'left')
```  
  
### Material properties parameters
   
  
```{r echo=FALSE} 

mat.df <- as.data.frame(cbind(Variable = c("Density contrast (g)",
                                      "Soundspeed contrast (h)",
                                      "Ambient Soundspeed (c)",
                                      "N body segment",
                                      "std(g)",
                                      "std(h)",
                                      "Correlation Length"),
                         Unit = c("ratio",
                                  "ratio",
                                  "m/s",
                                  "Integer",
                                  "std of ratio",
                                  "std of ratio",
                                  "% of L"),
                         Description = c("the ratio of the density of the animal to the density of the surrounding fluid",
                                         "the ratio of the sound speed in the animal to the sound speed in the surrounding fluid",
                                         "Soundspeed in surrounding fluid",
                                         "Defines the number of segments with different gi and hi along the body axis (>1 if an inhomogenous body should be computed).",
                                         
                                         "Standard deviation of the density (g), if an inhomogenous body should be computed",
                                         "Standard deviation of the sound speed contrast (h), if an inhomogenous body should be computed",
                                         "Controls the variability of g and h along the body axis (only xonsidered if the number of segments is >8)"),
                         Influence = c("Influences acoustic impedance, should be within [0.95, 1.05]",
                                       "Influences acoustic impedance, should be within [0.95, 1.05]",
                                       "","","","",""),
                         "Parameters name" =
                           c("...phy$g0",
                             "...phy$h0",
                             "...misc$cw",
                             "...phy$seg_no",
                             "...phy$g_std",
                             "...phy$h_std",
                             "...phy$corrL")
                         ))
knitr::kable(mat.df, keep.line.breaks = TRUE, style = 'grid', justify = 'left')
```  

### Simulation parameters  
  
```{r echo=FALSE} 

simu.df <- as.data.frame(cbind(Variable = c("Output",
                                      "Variable",
                                      "Sample points",
                                      "Integration Points",
                                      "Variable start value",
                                      "Variable end value",
                                      "Frequency"),
                         Unit = c("Selection",
                                  "Selection",
                                  "Integer",
                                  "Integer",
                                  "Float",
                                  "Float",
                                  "Float"),
                         Description = c("Model variable",
                                         "Number of output points along the variable maximum and minimum value",
                                         "Number of integration points along the target body",
                                         "Resolution of the model variable output",
                                         "Minimum output value",
                                         
                                         "Maximum output value",
                                         "Defines the discrete frequency for which the model is run if the variable is set to angle"),
                         Influence = c("1) backscattering amplitude; 2) differential backscattering cross-section [m2]; 3) Reduced Target Strength [dB re m2]; 4) Reduced Target Strength [db re m2]",
                                         "1) Frequency [kHz]; 2) Angle (°); 3) ka (wave number k * a)",
                                         "Resolution of the model variable output",
                                         "Resolution of the model shape input",
                                         
                                         "Range of the mdel output variable",
                                         "Range of the mdel output variable",
                                         "Center frequency of model variation around a range of theta"),
                         "Parameters name" =
                           c("...simu$out_indx",
                             "...simu$var_indx",
                             "...simu$n",
                             "...simu$ni",
                             "...simu$var0",
                             "...simu$var1",
                             "...simu$freq")
                         ))
knitr::kable(simu.df, keep.line.breaks = TRUE, style = 'grid', justify = 'left')
```  

## Changing the configuration parameters  

The configuration files can be changed either within a text editor or the different parameters can be directly changed within R:  

```{r echo=TRUE}
#Changing the length of the scattering target
message(paste("Old length:", para<img src="/docs/tex/1f082bcf5f8b37c5623142f728304d80.svg?invert_in_darkmode&sanitize=true" align=middle width=41.79045254999999pt height=22.831056599999986pt/>L))
para<img src="/docs/tex/1f082bcf5f8b37c5623142f728304d80.svg?invert_in_darkmode&sanitize=true" align=middle width=41.79045254999999pt height=22.831056599999986pt/>L <- 40
message(paste("New length:", para<img src="/docs/tex/1f082bcf5f8b37c5623142f728304d80.svg?invert_in_darkmode&sanitize=true" align=middle width=41.79045254999999pt height=22.831056599999986pt/>L))
#Changing the mean orientation of the scattering target
message(paste("Old orientation angle:", para<img src="/docs/tex/09f3d4efe0f39094be80c12bb0182f46.svg?invert_in_darkmode&sanitize=true" align=middle width=44.961343349999986pt height=21.68300969999999pt/>angm))
para<img src="/docs/tex/09f3d4efe0f39094be80c12bb0182f46.svg?invert_in_darkmode&sanitize=true" align=middle width=44.961343349999986pt height=21.68300969999999pt/>angm <- 30
message(paste("New orientation angle:", para<img src="/docs/tex/09f3d4efe0f39094be80c12bb0182f46.svg?invert_in_darkmode&sanitize=true" align=middle width=44.961343349999986pt height=21.68300969999999pt/>angm))
#Changing the density contrast
message(paste("Old density contrast:", para<img src="/docs/tex/0382bcc9ad1c11d1c5e92056961e3b85.svg?invert_in_darkmode&sanitize=true" align=middle width=26.39090684999999pt height=22.831056599999986pt/>g0))
para<img src="/docs/tex/0382bcc9ad1c11d1c5e92056961e3b85.svg?invert_in_darkmode&sanitize=true" align=middle width=26.39090684999999pt height=22.831056599999986pt/>g0 <- 1.031
message(paste("New density contrast:", para<img src="/docs/tex/0382bcc9ad1c11d1c5e92056961e3b85.svg?invert_in_darkmode&sanitize=true" align=middle width=26.39090684999999pt height=22.831056599999986pt/>g0))
#Changing the output start value
message(paste("Old output start value:", para<img src="/docs/tex/39e451ea59bcd04572867fa6085f35e8.svg?invert_in_darkmode&sanitize=true" align=middle width=37.21207874999999pt height=21.68300969999999pt/>var0))
para<img src="/docs/tex/39e451ea59bcd04572867fa6085f35e8.svg?invert_in_darkmode&sanitize=true" align=middle width=37.21207874999999pt height=21.68300969999999pt/>var0 <- 38
message(paste("New output start value:", para<img src="/docs/tex/39e451ea59bcd04572867fa6085f35e8.svg?invert_in_darkmode&sanitize=true" align=middle width=37.21207874999999pt height=21.68300969999999pt/>var0))
#Changing the output end value
message(paste("Old output end value:", para<img src="/docs/tex/39e451ea59bcd04572867fa6085f35e8.svg?invert_in_darkmode&sanitize=true" align=middle width=37.21207874999999pt height=21.68300969999999pt/>var1))
para<img src="/docs/tex/39e451ea59bcd04572867fa6085f35e8.svg?invert_in_darkmode&sanitize=true" align=middle width=37.21207874999999pt height=21.68300969999999pt/>var0 <- 200
message(paste("New output end value:", para<img src="/docs/tex/39e451ea59bcd04572867fa6085f35e8.svg?invert_in_darkmode&sanitize=true" align=middle width=37.21207874999999pt height=21.68300969999999pt/>var1))
```
  
  Alternatively, the settings can be loaded into the DWBAapp(), changed and saved from within the shiny app.  
  
## Using shape profiles or uniformely bent cylinder 
  
  Shape profiles can be used to define arbitrary shapes of the scattering target.  
  
The buildpos(para = list of parameters, disp_prof = 1 (include or exclude ggplot element) function can be used to generate shapes. Buildpos builds the coordinate vectors related to the shape positions along the z-axis. 
The buildpos function takes the following parameters from the parameters list:  

* shape<img src="/docs/tex/21fdc93e635e25b0b1b376f3ffa82909.svg?invert_in_darkmode&sanitize=true" align=middle width=223.77694679999996pt height=22.831056599999986pt/>ni - Number of integration points  
* shape<img src="/docs/tex/791c89d37c9c15614a1fcc85001c77b0.svg?invert_in_darkmode&sanitize=true" align=middle width=435.2939976pt height=24.65753399999998pt/>rho_L rho - L/radius of curvature (ignored if prof_name is given)  
* shape<img src="/docs/tex/0a2665289274495b1e4dff710b1bea38.svg?invert_in_darkmode&sanitize=true" align=middle width=596.70411735pt height=22.831056599999986pt/>axis_sm - smoothing along the x axis (uses smooth function)
* shape<img src="/docs/tex/482001d9d9a82dce85121878679477c2.svg?invert_in_darkmode&sanitize=true" align=middle width=1253.42179545pt height=323.83561649999996pt/>r(z)=a\sqrt{1-(\frac{2z}{L})^n}<img src="/docs/tex/0487b620f98e972c216789c1d8762f3a.svg?invert_in_darkmode&sanitize=true" align=middle width=33.28128374999999pt height=22.831056599999986pt/>z=\{-L/2│L/2\}<img src="/docs/tex/a118d8e597cf644dc4920f2d7d3b5e90.svg?invert_in_darkmode&sanitize=true" align=middle width=161.29733234999998pt height=22.831056599999986pt/>n=2<img src="/docs/tex/739b9e03f555ac28c4fcf9e0105a4279.svg?invert_in_darkmode&sanitize=true" align=middle width=33.28128374999999pt height=22.831056599999986pt/>L>2a<img src="/docs/tex/09ecc7660a2910f7b66d61c772030c1a.svg?invert_in_darkmode&sanitize=true" align=middle width=40.22766989999999pt height=22.831056599999986pt/>L<2a<img src="/docs/tex/568c4525a6659911fa4cdfd6cf27f053.svg?invert_in_darkmode&sanitize=true" align=middle width=566.4857582999999pt height=47.67123240000001pt/>shape<img src="/docs/tex/3f47776e1f582bb82b92c769ff4ed1e0.svg?invert_in_darkmode&sanitize=true" align=middle width=236.34555120000002pt height=24.65753399999998pt/>shape<img src="/docs/tex/df9cb62bcd928da2fc2fa471aafbe832.svg?invert_in_darkmode&sanitize=true" align=middle width=324.4628871pt height=24.65753399999998pt/>shape<img src="/docs/tex/3348dbaa3b17b6b464494f6eb9153373.svg?invert_in_darkmode&sanitize=true" align=middle width=73.70085689999999pt height=24.65753399999998pt/>plot

para<img src="/docs/tex/1f082bcf5f8b37c5623142f728304d80.svg?invert_in_darkmode&sanitize=true" align=middle width=41.79045254999999pt height=22.831056599999986pt/>order <- 200
para<img src="/docs/tex/1f082bcf5f8b37c5623142f728304d80.svg?invert_in_darkmode&sanitize=true" align=middle width=41.79045254999999pt height=22.831056599999986pt/>L_a <- 3
cyl <- buildpos(para)
message(paste("Length:",para<img src="/docs/tex/1f082bcf5f8b37c5623142f728304d80.svg?invert_in_darkmode&sanitize=true" align=middle width=41.79045254999999pt height=22.831056599999986pt/>L))
message(paste("L/a:",para<img src="/docs/tex/1f082bcf5f8b37c5623142f728304d80.svg?invert_in_darkmode&sanitize=true" align=middle width=41.79045254999999pt height=22.831056599999986pt/>L_a))
message(paste("Tapering order:",para<img src="/docs/tex/1f082bcf5f8b37c5623142f728304d80.svg?invert_in_darkmode&sanitize=true" align=middle width=41.79045254999999pt height=22.831056599999986pt/>order))
cyl<img src="/docs/tex/9a88e2ebea4d695414cff3a2e1bd66ad.svg?invert_in_darkmode&sanitize=true" align=middle width=27.40305974999999pt height=45.84475500000001pt/>shape<img src="/docs/tex/2b1438a3a260a291a654f0e5ec12ceb8.svg?invert_in_darkmode&sanitize=true" align=middle width=116.36816564999998pt height=22.831056599999986pt/>shape<img src="/docs/tex/f7f3aed21d4805ffde51835027139724.svg?invert_in_darkmode&sanitize=true" align=middle width=95.58364199999998pt height=22.465723500000017pt/>shape<img src="/docs/tex/0addd866b2dad8abad01ca9acd19e643.svg?invert_in_darkmode&sanitize=true" align=middle width=494.5415343pt height=24.65753399999998pt/>shape<img src="/docs/tex/3f47776e1f582bb82b92c769ff4ed1e0.svg?invert_in_darkmode&sanitize=true" align=middle width=236.34555120000002pt height=24.65753399999998pt/>shape<img src="/docs/tex/df9cb62bcd928da2fc2fa471aafbe832.svg?invert_in_darkmode&sanitize=true" align=middle width=324.4628871pt height=24.65753399999998pt/>shape<img src="/docs/tex/3348dbaa3b17b6b464494f6eb9153373.svg?invert_in_darkmode&sanitize=true" align=middle width=73.70085689999999pt height=24.65753399999998pt/>plot
```
  
  Input shape profiles must contain at least three columns with the center coordinates of each circular segment (X, Z) and radius of the circular segment (R). Two additional optional columns can be added to a shape file, the upper (Xupper -> X+R) and lower (Xlower -> X-R).  
  Some example shape profiles can be found in `r paste0(system.file(package="ZooScatR"),"/extdata/profiles")`  
  
Shape profiles can be loaded and the altered:  

```{r fig.width=8,fig.height=4}
# filenmae of an example configuration
fname <- paste0(system.file(package="ZooScatR"),"/extdata/configs/config_0.dat")
#Read the parameter file
para <- read_para(fname)
#set the profile filename
profname <- paste0(system.file(package="ZooScatR"),"/extdata/profiles/euphaus1.dat") #krill example
para<img src="/docs/tex/1f082bcf5f8b37c5623142f728304d80.svg?invert_in_darkmode&sanitize=true" align=middle width=41.79045254999999pt height=22.831056599999986pt/>prof_name <- profname
krill_shape1 <- buildpos(para)
krill_shape1<img src="/docs/tex/d49ad8d7404faaff766b441d28c54ec6.svg?invert_in_darkmode&sanitize=true" align=middle width=372.51250245pt height=45.84475500000001pt/>shape<img src="/docs/tex/3f9001b84dba2f5e773422d34f74fd07.svg?invert_in_darkmode&sanitize=true" align=middle width=423.8038398pt height=24.65753399999998pt/>plot

#change the axis smoothing, taper smoothing to some extreme values and L/a to obtian a more slender body
para<img src="/docs/tex/1f082bcf5f8b37c5623142f728304d80.svg?invert_in_darkmode&sanitize=true" align=middle width=41.79045254999999pt height=22.831056599999986pt/>L_a <- 30
para<img src="/docs/tex/1f082bcf5f8b37c5623142f728304d80.svg?invert_in_darkmode&sanitize=true" align=middle width=41.79045254999999pt height=22.831056599999986pt/>taper_sm <- 2000
para<img src="/docs/tex/1f082bcf5f8b37c5623142f728304d80.svg?invert_in_darkmode&sanitize=true" align=middle width=41.79045254999999pt height=22.831056599999986pt/>axis_sm <- 2000
krill_shape1 <- buildpos(para, disp_prof=1)
krill_shape1<img src="/docs/tex/5753f32c1174f088aa1dd1861dc71b0a.svg?invert_in_darkmode&sanitize=true" align=middle width=1838.99426865pt height=1073.4246567pt/><img src="/docs/tex/cd0a148f354d0c196f4fa762f49489bc.svg?invert_in_darkmode&sanitize=true" align=middle width=235.84486035pt height=45.84475499999998pt/><img src="/docs/tex/2e3724020dfd7378bb41e0ce660c93bf.svg?invert_in_darkmode&sanitize=true" align=middle width=8.21920935pt height=14.15524440000002pt/><img src="/docs/tex/3b6b6480dc04b7449560ac0b8fa8688e.svg?invert_in_darkmode&sanitize=true" align=middle width=94.29223649999999pt height=22.465723500000017pt/><img src="/docs/tex/658af11c138638f6629545423fe580ce.svg?invert_in_darkmode&sanitize=true" align=middle width=2957.3015735999998pt height=323.83561649999996pt/><img src="/docs/tex/728caa7601aaa6daba07f9706c837a96.svg?invert_in_darkmode&sanitize=true" align=middle width=178.31060775pt height=45.84475499999998pt/><img src="/docs/tex/2e3724020dfd7378bb41e0ce660c93bf.svg?invert_in_darkmode&sanitize=true" align=middle width=8.21920935pt height=14.15524440000002pt/><img src="/docs/tex/055821585fb67bb1cb31c0fb7f96eca8.svg?invert_in_darkmode&sanitize=true" align=middle width=94.29223649999999pt height=22.465723500000017pt/><img src="/docs/tex/b881bb3bc44aab5c5cc219fa7c4f0ea0.svg?invert_in_darkmode&sanitize=true" align=middle width=3195.9384336pt height=519.2694144pt/>\\frac{L}{a}$",
              "Orientation",
              "Density Contrast g", 
              "Sound Speed Contrast h",
              "Scattering model")
knitr::kable(gh)
#datatable(gh)
```
  
### Calculating soundspeed in water
  
ZooScatR includes routines to compute the soundspeed of the surrounding water following 3 methods:  

* Coppens [-@coppens_simple_1981]  
Calculates speed of sound in seawater based on Coppens (1981) The empirical equation generally holds validity for a temperature range between 0 and 35 degrees Celsius, Salinities between 0 and 45 parts per thousand and a depth range between 0 and 4000 m
Uses Depth (D in m), Salinity (S in ppt) and Temperature (C in Celsius) as input.  

<p align="center"><img src="/docs/tex/fd2fc0232665ce5c9fcfee383ef5cf1f.svg?invert_in_darkmode&sanitize=true" align=middle width=1198.13656875pt height=18.312383099999998pt/></p>  

Within ZooScatR:  
  
```{r}
c_Coppens1981(D=100,S=35,T=10)
```  
  
  
* MacKenzie [-@mackenzie_nine-term_1981]  
Calculate speed of sound in seawater based on MacKenzie (1981) The empirical equation generally holds validity for a temperature range between 2 and 30 degrees Celsius, Salinities between 25 and 40 parts per thousand and a depth range between 0 and 8000 m
Uses Depth (D in meters), Salinity (S in parts per thousands) and Temperature (T in degrees Celsius)  

<p align="center"><img src="/docs/tex/b4568421bb60ac809e77978b7e81dc5c.svg?invert_in_darkmode&sanitize=true" align=middle width=929.50204215pt height=18.312383099999998pt/></p>
  
Within ZooScatR:  

```{r}
c_Mackenzie1981(D=100,S=35,T=10)
```  
  
  
* Leroy [-@leroy_new_2008]  
Returns the sound speed according to Leroy et al (2008). This "newer" equation should solve the sound speed within 0.2 m/s for all seas, including the Baltic and Black sea, based on Temperature, Salinity and Latitude. Exceptions are some seas with anomalities close to the bottom. The equation was specifically designed to be used in marine acoustics.

Uses Depth (Z in m), Temperature (T in degrees Celsius), Salinity (S in parts per thousand) and Latitude (lat in degrees).  
<p align="center"><img src="/docs/tex/2db9c5fa5aadc55a71a6064667779042.svg?invert_in_darkmode&sanitize=true" align=middle width=1306.5301656pt height=18.312383099999998pt/></p>
  
Within ZooScatR:  

```{r}
c_Leroy08(Z=100,T=10,S=35,30)
```

### Calculating water density  

  Depending on the method used to compute the density contrast of the target to the surrounding fluid, the density rather then the density contrast might be obtained. In order to get the density contrast at ambient conditions, it is important to know the density of the surrounding fluid. Within ZooScatR the density of water can be calculated, following formulas found in the Tenth report of the joint panel on oceanographic tables and standards. UNESCO Technical Papers in Marine Science, Paris, 25p [@unesco_tenth_1981].  

Following the UNESCO Standard, density is calculated in four steps:  
  
  First the density of Standard Mean Ocean Water (<img src="/docs/tex/d36c16df9936469caf42c71dc677ffd8.svg?invert_in_darkmode&sanitize=true" align=middle width=50.137165649999986pt height=14.15524440000002pt/>) with temperature (T) in degree Celsius:
  <p align="center"><img src="/docs/tex/b5161933989c1774e037dbe2af8d1dfa.svg?invert_in_darkmode&sanitize=true" align=middle width=1243.9000859999999pt height=18.312383099999998pt/></p>
    
  Density at depth is dependent on the compressibility (<img src="/docs/tex/5c62da39aa7289df62d937cb24a31161.svg?invert_in_darkmode&sanitize=true" align=middle width=9.47111549999999pt height=14.15524440000002pt/>):  
  <p align="center"><img src="/docs/tex/b839e7e33d550a085fa09caa1cd6a341.svg?invert_in_darkmode&sanitize=true" align=middle width=2835.1904559pt height=18.905967299999997pt/></p>
  
  Then the density of seawater with Salinity (S in psu +/- ppm) at pressure (p in bar) = 0 is computed (<img src="/docs/tex/3ee3f93b7a51e5719c84fadc68137817.svg?invert_in_darkmode&sanitize=true" align=middle width=15.05143034999999pt height=14.15524440000002pt/>:  
  
  <p align="center"><img src="/docs/tex/23bdb7e7dafcda2a020d20980b020afb.svg?invert_in_darkmode&sanitize=true" align=middle width=1869.6127213500001pt height=18.312383099999998pt/></p>
    
Density at a given pressure is then computed as:  
<p align="center"><img src="/docs/tex/96ccac492a122d9ec50e175a77154dc0.svg?invert_in_darkmode&sanitize=true" align=middle width=108.20134875000001pt height=43.270631249999994pt/></p>

Within ZooScatR thde nsity can be computed through:  

```{r} rho(S=35,T=0.5,p=10) ```

or for surface density:   

```{r} 
rho(S=35, T=10)
#which is equal to:
rho_p0(S=35,T=10)
```  
  
The density of Standard Mean Ocean Water at a given temperature can be obtained through:  

```{r}
rho_smow(T=10)
```
## Running the model  
  Once all the parameters have been set, the DWBA model can be run with the defined parameters:  
  
```{r}
result <- bscat(para=para, misc=misc)
```
  
This returns a list of 6 with:  

* the variable values (var)  
* the model results (y)  
* a ggplot of the model output (rplot)  
* the name of the variable (xlab)  
* the caption of the y axis of the ggplot (ylab)  
* a ggplot of the shape input (shplot)
  
##References
