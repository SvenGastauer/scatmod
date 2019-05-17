#' @title Sound speed according to Mackenzie et al. (1981)
#' @description Calculate speed of sound in seawater based on MacKenzie (1981)
#' The empirical equation generally holds validity for a temperature range between 2 and 30 degrees Celsius, Salinities between 25 and 40 parts per thousand and a depth range between 0 and 8000 m
#' @source Mackenzie, K. V. (1981).
#' Nine term equation for sound speed in the oceans. The Journal of the Acoustical Society of America, 70(3), 807-812.
#' \url{http://asa.scitation.org/doi/abs/10.1121/1.386920}
#' @references Mackenzie, K. V. (1981).
#' Nine term equation for sound speed in the oceans. The Journal of the Acoustical Society of America, 70(3), 807-812.
#' @param D Depth in meters
#' @param S Salinity in parts per thousands
#' @param T Temperature in degrees Celsius
#' @examples
#' c_Mackenzie1981(100,35,10)
#' @export

c_Mackenzie1981 <- function(D,S,T){
  c<-1448.96 + 4.591*T - 5.304 *
    10^-2*(T^2) +
    2.374 * (10^-4)*(T^3) +
    1.340 * (S-35) +
    1.630 * (10^-2)*D +
    1.675 * (10^-7)*(D^2) - 1.025 * (10^-2)*T*(S - 35) - 7.139 * (10^-13)*T*(D^3)
return(c)
}

#' @title Sound speed according to Coppens et al. (1981)
#' @description Calculates speed of sound in seawater based on Coppens (1981)
#' The empirical equation generally holds validity for a temperature range between 0 and 35 degrees Celsius, Salinities between 0 and 45 parts per thousand and a depth range between 0 and 4000 m
#' @source Coppens, A. B. (1981).
#' Simple equations for the speed of sound in Neptunian waters. The Journal of the Acoustical Society of America, 69(3), 862-863.
#' \url{http://asa.scitation.org/doi/abs/10.1121/1.385486}
#' @references  Coppens, A. B. (1981).
#' Simple equations for the speed of sound in Neptunian waters. The Journal of the Acoustical Society of America, 69(3), 862-863.
#' @param D Depth in meters
#' @param S Salinity in parts per thousands
#' @param T Temperature in degrees Celsius
#' @examples
#' c_Coppens1981(D=100, S=35, T=10)
#' @export

c_Coppens1981 <- function(D,S,T){
  t <- T/10
  D = D/1000
  c0 <- 1449.05 + 45.7*t - 5.21*(t^2)  + 0.23*(t^3)  + (1.333 - 0.126*t + 0.009*(t^2)) * (S - 35)
  c <- c0 + (16.23 + 0.253*t)*D + (0.213-0.1*t)*(D^2)  + (0.016 + 0.0002*(S-35))*(S- 35)*t*D
  return(c)
}

#' @title Compute speed of sound according to Leroy et al. (2008)
#' @description Returns the sound speed according to Leroy et al (2008). This "newer" equation should solve the sound speed within 0.2 m/s for all seas, including the Baltic and Black sea, based on Temperature, Salinity and Latitude. Exceptions are some seas with anomalities close to the bottom. The equation was specifically designed to be used in marine acoustics.
#' @param Z Depth in m
#' @param S Salinity in parts per thousand
#' @param T Temperature in degrees Celsius
#' @param lat Latitude in degrees
#' @source Leroy, C. C., Robinson, S. P., & Goldsmith, M. J. (2008).
#' A new equation for the accurate calculation of sound speed in all oceans. The Journal of the Acoustical Society of America, 124(5), 2774-2782.
#' \url{http://asa.scitation.org/doi/abs/10.1121/1.2988296}
#' @references Leroy, C. C., Robinson, S. P., & Goldsmith, M. J. (2008).
#' A new equation for the accurate calculation of sound speed in all oceans. The Journal of the Acoustical Society of America, 124(5), 2774-2782.
#' @examples
#' # TABLE III in Leroy et al. (2008)
#' # Common oceans, lat = 30°, P= 80 MPa Z= 7808.13 m, S= 34.7%
#' lat=30; Z=7808.13; S=34.7; T=c(1,1.5,2,2.5,3)
#' c_Leroy08(Z,T,S,lat)
#' # Common oceans, lat = 30°, P= 80 MPa Z= 7808.13 m, T=2 °C
#' c_Leroy08(Z,T=2,S=seq(33.5,35.5,.5),lat)
#' # Common oceans, = 30°, P= 5 MPa Z= 497.12 m, S= 35%
#' c_Leroy08(Z=497.12,T=seq(-2,20,2),S=35,lat)
#' # Common oceans, = 30°, P= 5 MPa Z= 497.12 m, T=8 °C
#' c_Leroy08(Z=497.12,T=8,S=seq(33,37,1),lat)
#' @export
c_Leroy08 <- function(Z,T,S,lat){
  c <- 1402.5 + 5*T - 5.44 * 10^-2*T^2 + 2.1 * 10^-4*T^3 +
    1.33*S - 1.23 * (10^-2)*S*T+8.7*(10^-5)*S*T^2 +
    1.56*(10^-2)*Z+2.55*(10^-7)*Z^2-7.3*(10^-12)*Z^3+
    1.2*(10^-6)*Z*(lat-45)-9.5*(10^-13)*T*Z^3+
    3*(10^-7)*T^2*Z+1.43*(10^-5)*S*Z
  return(c)
}

