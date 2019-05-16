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
knitr::opts_chunk$set(collapse = T, comment = "#>")
options(tibble.print_min = 4L, tibble.print_max = 4L)
library(ZooScatR)
set.seed(1014)
```
This vignette will provide a brief description of the DWBA model used within the ZooScatR package, explain the needed input parameters and provide a few examples.  

## Quick Start

For a quick start, a minimal example:  
```{r fig.width=8,fig.height=4}
fname <- paste0(system.file(package="ZooScatR"),"/extdata/configs/config_0.dat") #Loacation of the parameters file
para = read_para(fname) #Read parameters file
#Create list with soundspeed info
misc <- list(cw=1500)
#Run DWBA based on config file
res <- bscat(para=para, misc=misc) #Target strength vs Frequency
res$rplot #Show the result plot
#Target strength vs angular position
para$simu$var_indx <- 2 #Set output variable to Angular position
#Run DWBA based on config file
res <- bscat(para=para, misc=misc)
res$rplot #Show the result plot
#Backscattering amplitude vs ka (Wavenumber x width)
para$simu$out_indx <- 1 #Set output to Backscattering amplitude
para$simu$var_indx <- 3 #Set output variable to ka
#Run DWBA based on config file
res <- bscat(para=para, misc=misc)
res$rplot #Show the result plot
#Reduced Target Strength vs Frequency (Wavenumber x width)
para$simu$out_indx <- 4 #Set output to Reduced Target Strength
para$simu$var_indx <- 1 #Set output variable to Frequency
#Run DWBA based on config file
res <- bscat(para=para, misc=misc)
res$rplot #Show the result plot
```

## The DWBA model - a brief explanation
A detailed description of the DWBA model and its application to the scattering properties of zooplankton can be found in  
The DWBA for a body of an arbitrary shape and size for an arbitrary frequency can be written as:
$$f_{bs} = \frac{k_s}{4}\int\int\int_v(\gamma_k - \gamma_{\rho})e^{2i\vec{k_b}\vec{r_v}}dv $$  

or under the simplified form for a deformed cylinder:    
$$f_{bs} = \frac{k_s}{4}\int_{\vec{r_{pos}}}a_c(\gamma_\kappa - \gamma_{\rho})e^{2i\vec{k_b}\vec{r_{pos}}}\frac{J_1(2k_ba_{c}cos\beta_{tilt})}{cos\beta_{tilt}} $$
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
```{r}
# filenmae of an example configuration
fname <- paste0(system.file(package="ZooScatR"),"/extdata/configs/config_0.dat")
#Read the parameter file
para <- read_para(fname)
```
  
the read_para function will load the model parameters as a list of 5:  

* ...$fname - Can be ignored in the scripting version but can be used within the DWBAapp()  
* ...$shape - Contains all the shape parameters  
* ...$orient - Contains the orientation parameters  
* ...$phy - Contains the material properties  
* ...$simu - Contains the simulation settings  

## The input parameters  
Based on the previously discussed parts of the equation and the structure of the parameters file, the DWBA takes four different categories of input parameters (shape, orientation, material properties and modelling parameters).  
  
A brief description, the input format, the influence of the parameter and its name within the parameter list are outlined below:  

###Shape parameters  

```{r echo=FALSE} 
para.df <- as.data.frame(cbind(Variable = c("Length(L)",
                                      "ρc/L",
                                      "L/a",
                                      "Taper order",
                                      "Length average",
                                      "std(L)/L",
                                      "Length increment",
                                      "Shape profile",
                                      "Taper smooth",
                                      "Axis smooth"),
                         Unit = c("mm",
                                  "ratio",
                                  "ratio",
                                  "float",
                                  "boolean",
                                  "mm",
                                  "mm",
                                  "filepath",
                                  "float",
                                  "float"),
                         Description = c("The total target body length",
                                         "Ratio of the radius of curvature (ρc) and L",
                                         "L/a with a the radius of the mid-point of the cylinder is the ratio of L to a",
                                         "The taper order (n) controls the tapering.",
                                         
                                         "The average model over a range of lengths will be produced",
                                         "The ratio of the standard deviation of length (std(L)) to the mean length (L)",
                                         "This value has to be chosen with care, as it has to be possible to calculate the provided std(L)/mean(L) around the provided mean L with the given increment.",
                                         "Path to a profile file containing 3 or 5 columns. (X, Z, R coordinates and optional Xupper Xlower). The profile file must contain at least 3 columns, containing the center coordinates (X, Z, R) of each circular segment",
                                         "Filter length to smooth the radius (R)",
                                         "Filter length to smooth the body axis (X, Z)"),
                         Influence = c("Length of the target",
                                       "Curvature of the bent cylinder, if no shape profile is loaded ( ∞ for straight cylinder)",
                                       "Contains information about the width of the target.",
                                       "For a straight cylinder (ρc/L -> infinity), n=2 results in a prolate spheroid if L>2a, or in an oblate spheroid for L<2a",
                                       "1 = perform average; 0 = No average",
                                       "Defines the variability of the target lengths, used to compute the input models for the averaged model output",
                                       "Defines the length increment of the target lengths, used to compute the input models for the averaged model output",
                                       "Defines the shape of the target, if no profile is selected a uniformly bent cylinder will be computed",
                                       "1 = no smoothing, otherwise smoothes the tapering (reduces complexity)",
                                       "1 = no smoothing, otherwise smoothens the axis (flatter)"),
                         "Parameters name" =
                           c("...shape$L",
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
message(paste("Old length:", para$shape$L))
para$shape$L <- 40
message(paste("New length:", para$shape$L))
#Changing the mean orientation of the scattering target
message(paste("Old orientation angle:", para$orient$angm))
para$orient$angm <- 30
message(paste("New orientation angle:", para$orient$angm))
#Changing the density contrast
message(paste("Old density contrast:", para$phy$g0))
para$phy$g0 <- 1.031
message(paste("New density contrast:", para$phy$g0))
#Changing the output start value
message(paste("Old output start value:", para$simu$var0))
para$simu$var0 <- 38
message(paste("New output start value:", para$simu$var0))
#Changing the output end value
message(paste("Old output end value:", para$simu$var1))
para$simu$var0 <- 200
message(paste("New output end value:", para$simu$var1))
```
  
  Alternatively, the settings can be loaded into the DWBAapp(), changed and saved from within the shiny app.  
  
## Using shape profiles or uniformely bent cylinder 
  
  Shape profiles can be used to define arbitrary shapes of the scattering target.  
  
The buildpos(para = list of parameters, disp_prof = 1 (include or exclude ggplot element) function can be used to generate shapes. Buildpos builds the coordinate vectors related to the shape positions along the z-axis. 
The buildpos function takes the following parameters from the parameters list:  

* shape$L - Length of the shape  
* shape$ni - Number of integration points  
* shape$order - Tapering order (ignored if prof_name is given)  
* shape$rho_L rho - L/radius of curvature (ignored if prof_name is given)  
* shape$prof_name - Custom shape, -1 for regular shape, filename for custom shape  
* shape$axis_sm - smoothing along the x axis (uses smooth function)
* shape$taper_sm - smooths the tapering (simplifies the shape)
  
The function outputs a list of 8:  

* r_pos  - Position vector   
* th_tilt - Angular information  
* dr  - distance vector  
* gamma_t - atan2(z, x)  
* taper - tapering  
* x - x coordinates (normalised by rho and L for unifomly bent cylinder, normalised for the number of integration points and L if a shape profile is loaded)  
* z - z coordinates (normalised by rho and L for unifomly bent cylinder, normalised for the number of integration points and L if a shape profile is loaded)  
* plot - a ggplot of the generated shape, included if disp_prof is set to 1  
  
  If no shape input is given, a uniformly bent cylinder with regular tapering will be used. Input parameters length (L), length/radius of curvature (rho_L), radius (a, taken from L/a -> L_a) and the tapering order (order)  are used to compute the cylinder. The tapering order (n) is defined through: 
$r(z)=a\sqrt{1-(\frac{2z}{L})^n}$  
with $z=\{-L/2│L/2\}$. For a prolate spheroid, $n=2$ with $L>2a$ while $L<2a$ results in an oblate spheroid.  
Some examples of prolate spheroids:  

```{r fig.width=6,fig.height=3}
cyl <- buildpos(para)
message(paste("Length:",para$shape$L))
message(paste("L/a:",para$shape$L_a))
message(paste("Tapering order:",para$shape$order))
cyl$plot

para$shape$order <- 200
para$shape$L_a <- 3
cyl <- buildpos(para)
message(paste("Length:",para$shape$L))
message(paste("L/a:",para$shape$L_a))
message(paste("Tapering order:",para$shape$order))
cyl$plot

para$shape$order <- 2
para$shape$L_a <- 2
para$shape$rhoL <- 200
cyl <- buildpos(para)
message(paste("Length:",para$shape$L))
message(paste("L/a:",para$shape$L_a))
message(paste("Tapering order:",para$shape$order))
cyl$plot
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
para$shape$prof_name <- profname
krill_shape1 <- buildpos(para)
krill_shape1$plot

#change the taper smoothing to some smoothing
para$shape$taper_sm <- 100
krill_shape1 <- buildpos(para)
krill_shape1$plot

#change the axis smoothing, taper smoothing to some extreme values and L/a to obtian a more slender body
para$shape$L_a <- 30
para$shape$taper_sm <- 2000
para$shape$axis_sm <- 2000
krill_shape1 <- buildpos(para, disp_prof=1)
krill_shape1$plot
```

##Changing the material properties and soundspeed  
  
  Soundspeed and density contrast (h & g) are important variables in the model. It has been suggested that the effects of varying g and h can be of the same order of magnitude as the orientation [@stanton_average_1993].  
  The DWBA model has been reported to perform well for g & h values within 1 +/- 5% (0.95 - 1.05), i.e. weak scatterers.  
  g & h can be either obtained experimentally or taken from literature values. The list below in a non-exhaustive list of g & h values found in literature. Large parts of the table are copied from Lavery et al. [-@lavery_determining_2007] and Lawson et al. [-@lawson_acoustically-inferred_2004].  
  
Some taxa are represented more than once, where multiple literature recodrings have been found. It is recommended to throughly study the cited and other literature before using any of the presented values.  
  
It should also be noted that L/a values might be fluctuating largely due to:

* geographical location [@kogeler_density-and_1987; @lawson_acoustically-inferred_2004]
* life history traits of the taxon or seasonality [@lawson_acoustically-inferred_2004; @kogeler_density-and_1987] 
  
  
g and h in some species have been reported to fluctuate with:  

* temperature [@chu_measurements_2005] 
* size classes [@chu_measurements_2005; @lawson_acoustically-inferred_2004; @kogeler_density-and_1987]  
* depth [@chu_measurements_2005]   
* seasonality (for example due to changes in lipid content) [@kogeler_density-and_1987]
* state of the analysed individuals (preseverd or alive) [@kogeler_density-and_1987].  

```{r, echo=FALSE}
taxa <- c("Euphausiids and Decapod Shrimp",
          "Larval Crustacean",
          "Amphipods",
          "Ostracods",
          "Chaetognaths and Polychaetes",
          "Gymnosome Pteropods (Clione)",
          "Salps",
          "Copepods",
          "Medusae",
          "Eggs",
          "Calanus finmarchicus",
          "Calanus hyperboreus",
          "Acartia clausi",
          "Calanus marshallae",
          "Meganyctiphanes norvegica",
          "Thysanoessa",
          "Calanus",
          "General",
          "Euphausia superba",
          "Euphausia crystallorophias",
          "Neocalanus cristatus",
          "Neocalanus plumchrus",
          "Ammodytes personatus (juvenile)",
          "Ammodytes personatus (adult)",
          "Salpa thompsoni")

La <- c("10.5",
        "2.55 [@lawson_acoustically-inferred_2004]",
        "3.00 [@lawson_acoustically-inferred_2004]",
        2.55,
        17.15,
        1.83,
        4.0,
        2.55,
        NA,
        NA,
        NA,
        NA,
        NA,
        NA,
        NA,
        NA,
        NA,
        NA,
        NA,
        NA,NA,NA,NA,NA,10)

Orientation <- c("N(20,20) [@benfield_estimating_2000], average ~0 [@lawson_improved_2006]",
                 "N(0.30) [@lawson_acoustically-inferred_2004]",
                 "N(0,30) [@lawson_acoustically-inferred_2004]",
                 "N(0,30)",
                 "N(0,30)",
                 "N(0,30)",
                 "N(0,30)",
                 "N(90,30)",
                 NA,
                 NA,
                 NA,
                 NA,
                 NA,
                 NA,
                 NA,
                 NA,
                 NA,
                 NA,
                 NA,
                 NA,
                 NA,
                 NA,
                 NA,
                 NA,"Uniform [0, π]")


g <- c("$$\\frac{5.485*L}{10^4}+1.002; L>25$$ $$1.016; L<25$$ [@lawson_acoustically-inferred_2004]",
       "1.058 [@lawson_acoustically-inferred_2004]",
       "1.058 [@lawson_acoustically-inferred_2004]",
       "1.03 [pers. comm. Dezhang Chu in @lavery_determining_2007]",
       "1.03 [pers. comm. Dezhang Chu in @lavery_determining_2007]",
       "1.03 [pers. comm. Dezhang Chu in @lavery_determining_2007]",
       "1.004 [@stanton_acoustic_1994]",
       "1.02 [pers. comm. Dezhang Chu in @lavery_determining_2007]",
       "1.02 [inferred from @monger_sound_1998 as reported in @lavery_determining_2007]",
       "0.979 [@chu_material_2003]",
       "1.025 - 1.029  g/cm^3^ depending on season [@kogeler_density-and_1987]",
       "1.022 - 1.036  g/cm^3^ depending on season [@kogeler_density-and_1987]",
       "1.04 g/cm^3^ [@greenlaw_acoustical_1979]",
       "1.04 g/cm^3^ [@greenlaw_acoustical_1979]",
       "1.057 g/cm^3^ [@kils_swimming_1981]",
       "1.052 - 1.074 g/cm^3^ depending on season and species [@kogeler_density-and_1987]",
       "1.022 - 1.036 g/cm^3^ depending on season and species [@kogeler_density-and_1987]",
       "0.9402 - 1.051 [@chu_measurements_2005]",
       "1.0241 [@chu_measurements_2005], 1.0357 [@foote_speed_1990]",
       "1.009 & 1.000 depth dependent [@chu_measurements_2005]",
       "0.997 - 1.009 [@matsukura_measurements_2009]",
       "0.995 - 1.009 [@matsukura_measurements_2009]",
       "1.021 [@yasuma_density_2009]",
       "1.032 [@yasuma_density_2009]",
       "1 - 1.0039 [@wiebe_acoustic_2009]"
       )



h <- c("$$\\frac{5.94*2L}{10^ 4}; L>25$$ $$1.019; L<25$$  [@lawson_acoustically-inferred_2004]",
       "1.058 [@lawson_acoustically-inferred_2004]",
       "1.058 [@lawson_acoustically-inferred_2004]",
       "1.03 [pers. comm. Dezhang Chu in @lavery_determining_2007]",
       "1.03 [pers. comm. Dezhang Chu in @lavery_determining_2007]",
       "1.03 [pers. comm. Dezhang Chu in @lavery_determining_2007]",
       "1.004 [@stanton_acoustic_1994]",
       "1.058 [@chu_inference_2000]",
       "1.02 [inferred from @monger_sound_1998 as reported in @lavery_determining_2007]",
       "1.017 [@stanton_simple_1989]",
       "1.027 (mixture C. finmarchicus and C. hyperboreus) [@kogeler_density-and_1987]",
       "1.027 (mixture C. finmarchicus and C. hyperboreus) [@kogeler_density-and_1987]",
       "NA",
       "1.007 [@kogeler_density-and_1987]",
       "1.030 [@kogeler_density-and_1987]",
       "1.026 [@kogeler_density-and_1987]",
       "1.027 [@kogeler_density-and_1987];  0.949 & 1.013 - Depth dependent [@chu_measurements_2005]",
       "0.949 - 1.096 [@chu_measurements_2005]",
       "1.031 [@chu_measurements_2005], 1.0279 [@foote_speed_1990]",
       "1.025 & 1.029 depth dependent [@chu_measurements_2005]",
       "1.013 - 1.025 [@matsukura_measurements_2009]",
       "1.006 - 1.021 [@matsukura_measurements_2009]",
       "1.02 [@yasuma_density_2009]",
       "1.02 [@yasuma_density_2009]",
       "1.006 - 1.0201 [@wiebe_acoustic_2009]")


model <- c("DWBA uniformly-bent cylinder","DWBA uniformly-bent cylinder","DWBA uniformly-bent cylinder","DWBA uniformly-bent cylinder","DWBA uniformly-bent cylinder","DWBA uniformly-bent cylinder","DWBA uniformly-bent cylinder","DWBA prolate spheroid", "DWBA two prolate spheroid surfaces", "High-pass fluid sphere","NA","NA","NA","NA","NA","NA","NA",NA,NA,NA,"DWBA Deformed Cylinder","DWBA Deformed Cylinder",NA,NA,"DWBA")

gh <- as.data.frame(cbind(taxa,La,Orientation,g,h,model))
names(gh)<- c("Taxon",
              "Length-to-girth ratio $\\frac{L}{a}$",
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

$$t = T/10; D = D/1000 \\
c_0 = 1449.05 + 45.7t - 5.21 t^2 + 0.23 t^3 + (1.333 - 0.126 t + 0.009 t^2) (S - 35) \\
c = c_0 + (16.23 + 0.253t) D + (0.213 - 0.1t) * D^2 + (0.016 + 2e^{-04} (S - 35)) (S - 35)tD$$  

Within ZooScatR:  
  
```{r}
c_Coppens1981(D=100,S=35,T=10)
```  
  
  
* MacKenzie [-@mackenzie_nine-term_1981]  
Calculate speed of sound in seawater based on MacKenzie (1981) The empirical equation generally holds validity for a temperature range between 2 and 30 degrees Celsius, Salinities between 25 and 40 parts per thousand and a depth range between 0 and 8000 m
Uses Depth (D in meters), Salinity (S in parts per thousands) and Temperature (T in degrees Celsius)  

$$1448.96 + 4.591 T - 5.304 10^{-2} T^2 + 2.374 *10^{-4} T^3 +\\ 
1.34 (S - 35) + 1.63 * 10^{-2}D + 1.675 * 10{^-7} D^2 - \\
1.025 * 10^{-2} T (S -35)-7.139 * 10^{-13}  T  D^3$$
  
Within ZooScatR:  

```{r}
c_Mackenzie1981(D=100,S=35,T=10)
```  
  
  
* Leroy [-@leroy_new_2008]  
Returns the sound speed according to Leroy et al (2008). This "newer" equation should solve the sound speed within 0.2 m/s for all seas, including the Baltic and Black sea, based on Temperature, Salinity and Latitude. Exceptions are some seas with anomalities close to the bottom. The equation was specifically designed to be used in marine acoustics.

Uses Depth (Z in m), Temperature (T in degrees Celsius), Salinity (S in parts per thousand) and Latitude (lat in degrees).  
$$ 1402.5 + 5 T - 5.44 * 10^{-2} T^2 + 2.1 * 10^{-4} T^3 + 1.33 S -\\ 
        1.23 * 10^{-2} S T + 8.7 * 10^{-5} S T^2 + \\
        1.56 * 10^{-2} Z + 2.55 * 10^{-7} Z^2 - \\
        7.3 * 10^{-12} Z^3 + 1.2 * 10^{-6} Z (lat - 45) -\\ 
        9.5 * 10^{-13} T Z^3 + 3 * 10^{-7} T^2 Z + 1.43 10^{-5} S Z$$
  
Within ZooScatR:  

```{r}
c_Leroy08(Z=100,T=10,S=35,30)
```

### Calculating water density  

  Depending on the method used to compute the density contrast of the target to the surrounding fluid, the density rather then the density contrast might be obtained. In order to get the density contrast at ambient conditions, it is important to know the density of the surrounding fluid. Within ZooScatR the density of water can be calculated, following formulas found in the Tenth report of the joint panel on oceanographic tables and standards. UNESCO Technical Papers in Marine Science, Paris, 25p [@unesco_tenth_1981].  

Following the UNESCO Standard, density is calculated in four steps:  
  
  First the density of Standard Mean Ocean Water ($\rho_smow$) with temperature (T) in degree Celsius:
  $$a0 = 999.842594 \\
    a1 = 6.793953 * 10^-2 \\
    a2 = -9.09529 * 10^-3 \\
    a3 = 1.001685 * 10^-4 \\
    a4 = -1.120083 * 10^-6 \\
    a5 = 6.536332 * 10^-9 \\
    \rho_{smow}(T) = a0 + a1 * T + a2 * T^2 + a3 * T^3 + a4 * T^4 + a5 * T^5$$
    
  Density at depth is dependent on the compressibility ($\kappa$):  
  $$ h_0 = 3.2399 \\
    h_1 = 1.43713 * 10^{-3} \\
    h_2 = 1.16092 * 10^{-4} \\
    h_3 = -5.77905 * 10^{-7} \\
    i_0 = 2.838 * 10^{-3} \\
    i_1 = -1.0981 * 10^{-5} \\
    i_2 = -1.6078 * 10^{-6} \\
    j_0 = 1.91075 * 10^{-4} \\
    k_0 = 8.50935 * 10^{-5} \\
    k_1 = -6.12293 * 10^{-6} \\
    k_2 = 5.2787 * 10^{-8} \\
    m_0 = -9.9348 * 10^{-7} \\
    m_1 = 2.0816 * 10^{-8} \\
    m_2 = 9.1697 * 10^{-10} \\
    B_w = k_0 + k_1 T + k_2 T^2 \\
    B_2 = B_w + (m_0 + m_1 T + m_2 T^2) S \\
    A_w = h_0 + h_1 T + h_2 T^2 + h_3 T^3 \\
    A_1 = A_w + (i_0 + i_1 T + i_2T^2) S + j_0 S^{1.5} \\
    K_{p0}(S, T) + A_1 p + B_2 * p^2 $$
  
  Then the density of seawater with Salinity (S in psu +/- ppm) at pressure (p in bar) = 0 is computed ($\rho_0$:  
  
  $$b_0 = 8.2449 * 10^-1 \\
    b_1 = -4.0899 * 10^-3 \\
    b_2 = 7.6438 * 10^-5 \\
    b_3 = -8.2467 * 10^-7 \\
    b_4 = 5.3875 * 10^-9 \\
    c_0 = -5.7246 * 10^-3 \\
    c_1 = 1.0227 * 10^-4 \\
    c_2 = -1.6546 * 10^-6 \\
    d_0 = 4.8314 * 10^-4 \\
    B_1 = b_0 + b_1 T + b_2 T^2 + b_3 T^3 + b_4 T^4 \\
    C_1 = c_0 + c_1 T + c_2 T^2 \\
    \rho_0(S,T)=\rho_{smow}(T) + B_1 S + C_1 * S^{1.5} + d_0 S^2 $$
    
Density at a given pressure is then computed as:  
$$ \rho = \frac{\rho_o(S,T)}{1-\frac{p}{K(S,T)}}$$

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
