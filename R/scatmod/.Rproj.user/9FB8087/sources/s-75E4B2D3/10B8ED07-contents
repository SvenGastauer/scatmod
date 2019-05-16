#'Calculate the acoustic wave length lambda
#' @param c Soundspeed in m/s
#' @param f frequency in Hz (s^-1)
#' @examples
#' lambda(c=1500,f=200000)
#' @export
lambda <- function(c,f) {c/f}

#'Calculate the acoustic wavenumber k
#' @param c Soundspeed in m/s
#' @param f frequency in Hz (s^-1)
#' @examples
#' k(c=1500,f=200000)
#' @export
k <- function(c,f){2 * pi / lambda(c,f)}

#' Spherical bessel function first kind
#' @param x numeric data vector
#' @param order order of the bessel funciton
#' @examples
#' Sbessj(x=1:10,order=1)
#' @export
Sbessj <- function(x,order){
  sqrt(pi/2) * 1/sqrt(x) * besselJ(x,(order + (1/2)))
}

#' Spherical bessel function second kind (Neumann)
#' @param x numeric data vector
#' @param order order of the bessel funciton
#' @examples
#' Sneum(x=1:10,order=1)
#' @export
Sneum <- function(x,order){
  sqrt(pi/2) * 1/sqrt(x) * besselY(x,(order + 1/2))
}

#' Derivative of the Spherical bessel function second kind
#' @param x numeric data vector
#' @param order order of the bessel funciton
#' @examples
#' Sneum_p(x=1:10,order=1)
#' Sneum_p(x=1:10,order=0)
#' @export
Sneum_p <- function(x,order){
  sn <- Sneum(x,order)

  if(order==0){
    sp1 <- sqrt(pi/(2*x))*besselY(x, order+3/2)
    return((order/x) * sn - sp1)
  }else{
    sm1 <- sqrt(pi/(2*x))*besselY(x, order-1/2)
    return(sm1 - ((order+1)/x) * sn)
  }
}

#' Derivative of the Spherical bessel function first kind
#' @param x numeric data vector
#' @param order order of the bessel funciton
#' @examples
#' Sbessj_p(x=1:10,order=1)
#' Sbessj_p(x=1:10,order=0)
#' @export
Sbessj_p <- function(x,order){
  bn <- Sbessj(x,order)
  bn <- (sqrt(pi/(2*x)))*besselJ(x, order+0.5)

  if(order==0){
    bp1 <- (sqrt(pi/(2*x)))*besselJ(x, order+3/2)
    return((order/x) * bn - bp1)
  }else{
    bm1 <- sqrt(pi/(2*x))*besselJ(x, order-1/2)
    return(bm1 - ((order+1)/x) * bn)
  }
}

#' Hankel function
#' @param k kind of Hankel function must be 1 or 2
#' @param n order of the Hankel funciton
#' @param z numeric data vector
#' @examples
#' besselH(k=1,n=1,z=1:10)
#' @export
besselH <- function(k,n,z){
  if(!(k %in% c(1,2))){
    message("The kind of the Hankel function must be 1 or 2")
    return()
  }
  if(k==1){bh<-besselJ(z,n) + 1i*besselY(z,n)}
  if(k==2){bh<-besselJ(z,n) - 1i*besselY(z,n)}
  return(bh)
}



#' Spherical Hankel function
#' @param z numeric data vector
#' @param order order of the bessel funciton
#' @examples
#' SHankel(x=1:10,order=1)
#' SHankel(x=1:10,order=0)
#' @export
SHankel<- function(z,order){
  (sqrt(pi/(2*x))) * besselH(k=1,z=z,rep(order+1/2,length(x)))
}

#' Derivative of the Spherical Hankel function
#' @param x numeric data vector
#' @param order order of the bessel funciton
#' @examples
#' SHankel_p(x=1:10,order=1)
#' SHankel_p(x=1:10,order=0)
#' @export
SHankel_p <- function(x,order){
  if(order == 0){
    Hankel_n = (sqrt(pi/(2*x)))* besselJ(x,order+1/2) +
      1i*(sqrt(pi/(2*x)))* besselY(x,order+1/2)
    Hankel_nplus1 = (sqrt(pi/(2*x)))* besselJ(x,order+3/2) +
      1i*(sqrt(pi/(2*x)))* besselY(x,order+3/2)
    SphHankel_deriv = (order/x)*Hankel_n - Hankel_nplus1
  }else if(order > 0){
    #Spherical Bessel functions of other order are directly calculated
    #here to try and reduce the number of function calls
    Hankel_n = (sqrt(pi/(2*x)))* besselJ(x,order+1/2)+
      1i*(sqrt(pi/(2*x)))* besselY(x,order+1/2);
    Hankel_ntake1 = (sqrt(pi/(2*x)))* besselJ(x,order-1/2) +
      1i*(sqrt(pi/(2*x)))* besselY(x,order-1/2);

    SphHankel_deriv <- Hankel_ntake1 - ((order+1)/x)*Hankel_n;
  }
  return(SphHankel_deriv)
}

#' Calculate Legendre Polynomial
#' @description Function to calculate the Legendre Polynomial,
#' based on the recurrence relation in Numerical Recipes in C (Eq. 4.6.10) with j = j-1
#' Therefore:
#' P_j = (2j-1) * P_(j-1) - (j-1) * P_(j-2)
#' P_0 = 1; P_1 = x
#'
#' @param degree The degree of the desired polynomial
#' @param coeffs the values at which the p[olynomial will be evaluated
#' @return Legendre polynomials
#' @examples
#' coeffs=2;degree=3
#' LegPoly(degree,coeffs)
#' @export
LegPoly <- function(degree, coeffs){
  lp <- matrix(1,dim(matrix(coeffs))[2], dim(matrix(coeffs))[1])
  lp1 <- coeffs * lp

  if(degree==1){
    return(lp1)
  }

  if (degree > 1){
    for(cntr in 2:degree){
      lp2 <- ((coeffs * (2*cntr-1) * lp1 - (cntr - 1) * lp)/cntr)
      lp <- lp1
      lp1 <- lp2
    }
    return(lp2)
  }else{
    return(matrix(1,dim(matrix(coeffs))[2], dim(matrix(coeffs))[1]))
  }
}


#' Calculate the analytical solution for a weakly scattering sphere
#' @description Scattered pressure from an incident plane wave upon a fluid sphere. Based on:
#' Jech, J. M., Horne, J. K., Chu, D., Demer, D. A., Francis, D. T., Gorska, N., ... & Reeder, D. B. (2015).
#' "Comparisons among ten models of acoustic backscattering used in aquatic ecosystem research."
#' The Journal of the Acoustical Society of America, 138(6), 3742-3764.
#' modified from:
#' Anderson, V. C. (1950). "Sound scattering from a fluid sphere."
#' The Journal of the Acoustical Society of America, 22(4), 426-431.
#' @param f Frequency in Hz (s^-1)
#' @param r Range in m from center of sphere
#' @param a Radius of sphere
#' @param c Soundspeed in surrounding fluid m/s
#' @param h Soundspeed contrast inside/surrounding fluid
#' @param g Density contrast inside/surrounding fluid
#' @param rho Density of surrounding fluid
#' @examples
#' fs <- as.list(seq(10,400, by=1)*1000) #Frequencies
#' r <- 10 #range
#' a <- 0.01 # radius
#' c <- 1477.4 #soundspeed surrounding fluid
#' rho <- 1026.8 #density surrounding fluid
#' g <- 1028.9/rho #density contrast
#' h <- 1480.3/c #soundspeed contrast
#' TS <- sapply(fs,TS.sphere2,r=r,a=a,c=c,h=h,g=g,rho=rho)
#' plot(fs,TS, type="l", xlab="Frequency [Hz]",ylab="TS [dB re m2]")
#' @export
TS.sphere <- function(f,r,a,c,h,g, rho){

  ###Basic calculations

  #External fluid
  k0 <- k(c,f) #Wavenumber surrounding fluid
  kr <- k0 * r #Wavenumber surrounding fluid * range
  ka <- k0 * a #Wavenumber surrounding fluid * radius
  rho_c <- rho * c #rho external fluid * soundspeed

  #Internal fluid
  k1 <- k(h*c,f) #Wavenumber internal fluid
  k1a <- k1 * a  #Wavenumber internal fluid * radius
  #rho1 <- g *rho #density internal fluid


  Cn_fun <- function(n){
    ((Sbessj_p(k1a,n)*Sneum(ka,n))/(Sbessj(k1a,n)*Sbessj_p(ka,n)) -
       g*h*(Sneum_p(ka,n)/Sbessj_p(ka,n))) /
      ((Sbessj_p(k1a,n)*Sbessj(ka,n))/(Sbessj(k1a,n)*Sbessj_p(ka,n)) - g*h)
  }
  n <- seq(0,round(ka+20,0))
  Cn <- apply(matrix(n),1,Cn_fun)

  A <- -1/(1+1i*Cn)
  fbs <- -1i/k0*sum((-1)^n * (2*n +1) * A)
  TS <- 10*log10(abs(fbs)^2)
  return(TS)
}
