---
title: "Compare the ZooScatR DWBA to an analytical solution"
author: "Sven Gastauer"
date: "`r Sys.Date()`"
bibliography: vignettes.bib
output:
  rmarkdown::html_vignette:
    toc: true
    toc_depth: 4
vignette: >
  %\VignetteIndexEntry{Compare the ZooScatR DWBA to an analytical solution}
  %\usepackage[utf8]{inputenc}
  %\VignetteEngine{knitr::rmarkdown}
---
This document compares the results of the the DWBA implementation in ZooScatR to an anlytical scattering model of a sphere [@anderson_sound_1950], following routines described in Jech et al. [-@jech_comparisons_2015].

This vignette requires the ZooScatR package for the implementation of the DWBA model, ggplot2 for plotting, viridis for nicer colors.

```{r warning=FALSE}
library(ZooScatR)
library(ggplot2)
library(viridis)
```
## The analytical model of a sphere  

For the purpose of this example we will build the general anlytical model for a scattered wave by a sphere [@anderson_sound_1950]:  
$$p_{scat}=p_0\sum^{\infty}_{n=0}A_n(2n+1)P_n (cos\theta)h^1_n (k_w r)$$  
with   

* the range ($r$ in [m])  
* the acoustic wavenumber in the surrounding water($k_w$)  
* $k=\frac{2\pi}{\lambda}$  
* wavelength $\lambda=\frac{f}{c}$ in [m]  
* $f$ is the frequency in $Hz =s^{-1}$  
* $c$ is the soundspeed in $\frac{m}{s}$)  
* $p_0$ is the incident pressure  
* $A_n$ is defined by the boundary conditions [@anderson_sound_1950]. For $A_n$, definitions following [@jech_comparisons_2015] were used, rather than [@anderson_sound_1950].  
* $P_n$ is the Legendre polynomial with degree $n$  
* $h^1_n$ is the spherical Hankel function of the first kind or the spherical Bessel function of thrid the kind  
* $\theta$ is the scattering angle  
  
  For backscatter $\theta=\pi$; therefore $P_n$ becomes $P_n(-1)=(-1)^n$.  
  
  In the farfield 
  $$
  \begin{aligned}
  k_wr \gg 1, \\
  h^1_n(k_wr) \xrightarrow[k_wr\gg1]{} \frac{[(-i)^{n+1}]}{(k_wr)}e^{ik_wr}
  \end{aligned}
  $$  
  the acoustic backscatter pressure $p_{bs}$ can be expressed as a function of backscattering amplitude ($f_{bs}$, incident pressure, phase and range:  
  $$p_{bs}=p_0 \frac{e^{ik_w r}}{r}f_{bs}$$  
  with the simplified $f_bs$ becoming:  
  $$f_{bs}=-\frac{i}{k_w}\sum^{\infty}_{n=0}(-1)^n(2n+1)A_n $$
  following Jech et al. [-@jech_comparisons_2015], $n$ was limited to the nearest integer of $||k_wa||+20$, providing a precision of 0.1 dB.  
  
  From $f_bs$, target strength $TS$ in $dB \text{ re }m^2$ can be computed as [@anderson_sound_1950]:  
  $$TS = 10log_{10}(|f_bs|^2)$$  
    
  For a fluid filled sphere, the coefficient, the coefficient $A_n$ can be computed as:  
  $$A_n=\frac{-1}{1+iC_n}$$  
  and  
  $$C_n = \frac{\frac{[j'_n(k_1a)y_n(ka)]}{[j_n(k_1a)j'_n(ka)]} - gh\frac{y'_n(ka)}{j'_n(ka)}}{\frac{[j'_n(k_1a)j_n(ka)]}{[j_n(k_1a)j'_n(ka)]}-gh}$$
  with:  
  
  * $k_1$ the wavenumber inside the fluid-filled sphere  
  * $g$ the density contrast for the density $[\frac{kg}{m^3}]$ inside the sphere ($\rho_t$) and in the surrounding fluid ($\rho_w$)  
  * $h$ the soundspeed contrast for the soundspped $[\frac{m}{s}]$ inside the sphere ($c_t$) and in the surrounding fluid ($c_w$)  
  * $y$ is the spherical Neumann function  
  
  Letting $gh \rightarrow \infty$ results in a rigid sphere and:  
  $$A_n=-\frac{j'_n(k_wa)}{h'_n(k_wa)}$$  
  Similarly, letting $gh \rightarrow 0$ results in a pressure release sphere and:
  $$A_n=-\frac{j_n(k_wa)}{h_n(k_wa)}$$  
  
  These functions have been implemented within ZooScatR and can be called using:  
  
```{r}
library(ZooScatR)
r <- 10 #range 
a <- 0.01 # radius
c <- 1477.4 #soundspeed surrounding fluid
rho <- 1026.8 #density surrounding fluid
g <- 1028.9/rho #density contrast
h <- 1480.3/c #soundspeed contrast
f <- 200 * 1000 #Frequency in Hz

TS.sphere2(f=f,r=r,a=a,c=c,h=h,g=g,rho=rho)
```
  
  Note: Results involving Bessel functions have to be used with a bit of caution. Given the diffrent ways available to compute the Bessel functions slight variations occur for example between results obtained in Matlab and R. Generally the fluctuations are relatively small (within a fraction of 1%), but they are noticeable.  
  
###Settings for a weakly scattering sphere

The following settings were used for a weakly scattering sphere, as defined in [@jech_comparisons_2015]:  

```{r}
r <- 10 #range 
a <- 0.01 # radius
c <- 1477.4 #soundspeed surrounding fluid
rho <- 1026.8 #density surrounding fluid
g <- 1028.9/rho #density contrast
h <- 1480.3/c #soundspeed contrast

#Frequency range
fmin=12
fmax=400
freqs <- seq(fmin,fmax, by=1)
```

Set the settings inside ZooScatR:  

```{r}
fname <- paste0(system.file(package="ZooScatR"),"/extdata/configs/config_0.dat") #Loacation of the parameters file
para = read_para(fname) #Read parameters file

#Create list with soundspeed info
misc <- list(cw=c) #Set soundspeed in the surrounding fluid

#Set the material properties
para$phy$g0 <- g #set the density contrast
para$phy$h0 <- h #set the soundspeed contrast

#set the simulation parameters
para$simu$var0<-fmin #Set the minimum frequency
para$simu$var1<-fmax #Set the maximum frequency
para$simu$n=length(freqs) #Set the number of output points
para$simu$ni=2000 #any high number

```

## Building a sphere inside ZooScatR

```{r warning=FALSE,fig.width=8,fig.height=4}
#Set the shape parameters
para$shape$L <- 2*1000*a # 2 * the radius in m to get length in mm
para$shape$order <- 2 #Set the tapering order
para$shape$L_a <- 2 #Set L/a
para$shape$rho_L <- 2000 #any high number to get a high curvature

#Build the sphere and plot the result
sp <- buildpos(para) #build the shape
sp$plot #show the shape plot
```

## Run the different models

Run the analytical model:  

```{r warning=FALSE,fig.width=8,fig.height=4}
fs <- as.list(freqs*1000) #Create a list of frequencies
TS.MJ <- sapply(fs,TS.sphere2,r=r,a=a,c=c,h=h,g=g,rho=rho) #Apply frequency list to the analytical model
```
  
Run the ZooScatR DWBA:  

```{r warning=FALSE,fig.width=8,fig.height=4}
#Run DWBA based on config file
DWBA <- bscat(para=para, misc=misc)
#Show the model outcome
DWBA$rplot

```
  
  Build a function to compute and plot the error:  
  The error is computed following Jech et al. [-@jech_comparisons_2015] as:  
  $$|\overline{\Delta TS}|=\frac{1}{N}\sum^N_{i=1}|TS_{i. predicted}-TS_{i-benchmark}| $$
  with $N$ the number of sample points (frequency points).  
  
  
```{r warning=FALSE,fig.width=8,fig.height=4,tidy=TRUE}
#Compare results
TS.comp<-function(TS1,TS2,freqs){
  require(ggplot2)
  require(viridis)
  TScomp <- as.data.frame(cbind(TS = c(TS1,TS2),
                 Freq = rep(freqs,2),
                 Model=rep(c("Analytical","DWBA"),each=length(freqs))))
  names(TScomp)<- c("TS","Frequency","Model")
  TScomp$TS <- as.numeric(as.character(TScomp$TS))
  TScomp$Frequency <- as.numeric(as.character(TScomp$Frequency))
  
  err <- sum(abs(TS1-TS2))/length(freqs)
  TScomp$diff <- rep(abs(TS1-TS2),2)
  message(paste("Overall error:", round(mean(err),2),"dB"))
  #ggplot remove backgorund
  rmb <- theme(axis.line = element_line(colour = "black"),
    panel.grid.major = element_blank(),
    panel.grid.minor = element_blank(),
    panel.border = element_blank(),
    panel.background = element_blank())
  
  print(ggplot(data=TScomp,aes(x=Frequency,y=TS, group=Model,col=Model))+
          geom_line(lwd=1)+
          scale_color_brewer(palette="Set1")+
          theme(legend.position = "top")+
          xlab("Frequency [kHz]")+
          rmb)
  print(ggplot(data=TScomp,aes(x=Frequency,y=diff, col=diff))+
          geom_line(lwd=1.2)+
          scale_color_viridis(name="dB difference")+
          theme(legend.position="top")+xlab("Frequency [kHz]")+rmb)
  return(TScomp)
}
```
  
  Run the error function for the anylitcal and modelled solutions:  
  
```{r warning=FALSE,fig.width=8,fig.height=4}  
TS.compare <- TS.comp(TS.MJ,DWBA$y,freqs)
```
    
For a weak scattering sphere, the error is mostly below 1%. Only within the null locations, the error increases, while th elocations of the nulls are good.  
  
Running the model for material properties of krill as reported in Calie et al. [-@calise_sensitivity_2011] in this example we are looking at a hypothetical perfectly round krill with a radius of 3 mm:  

```{r}
a <- 0.01
g <- 1.0357 #density contrast
h <- 1.0279 #soundspeed contrast
c <- 1456

#Set the material properties in ZooScatR
para$shape$L <- 2*1000*a # 2 * the radius in m to get length in mm
para$phy$g0 <- g #set the density contrast
para$phy$h0 <- h #set the soundspeed contrast
misc$cw <- c

#Run the analytical model
TS.MJ <- sapply(fs,TS.sphere2,r=r,a=a,c=c,h=h,g=g,rho=rho) #Apply frequency list to the analytical model

#Run the ZooScatR DWBA:  
DWBA <- bscat(para=para, misc=misc)
```
  
Compare the results:   

```{r warning=FALSE,fig.width=8,fig.height=4}  
TS.compare <- TS.comp(TS.MJ,DWBA$y,freqs)
```  


Compare for TS > -80:   

```{r warning=FALSE}
th <- - 80
tmp1 <- TS.MJ
tmp1[which(tmp1 < th)] <- th
tmp2 <- DWBA$y
tmp2[which(tmp2 < th)] <- th
Ts.compare2 <- TS.comp(tmp1,tmp2,freqs)
```
   The ZooScatR DWBA model performs well for the material preperties of krill, when compared to the analytical model.

  
Running the model for very strong scatterer like a 38.1 mm tungsten-carbide sphere:  

```{r}
a <- 0.0381
g <- 14900/rho #density contrast
h <- 6853/c #soundspeed contrast

#Set the material properties in ZooScatR
para$shape$L <- 2*1000*a # 2 * the radius in m to get length in mm
para$phy$g0 <- g #set the density contrast
para$phy$h0 <- h #set the soundspeed contrast

#Run the analytical model
TS.MJ <- sapply(fs,TS.sphere2,r=r,a=a,c=c,h=h,g=g,rho=rho) #Apply frequency list to the analytical model

#Run the ZooScatR DWBA:  
DWBA <- bscat(para=para, misc=misc)
```
  
Compare the results:   

```{r warning=FALSE,fig.width=8,fig.height=4}  
TS.compare <- TS.comp(TS.MJ,DWBA$y,freqs)
```  
   
   The ZooScatR DWBA model holds no validity for such strong scatterers.  
   
##References
