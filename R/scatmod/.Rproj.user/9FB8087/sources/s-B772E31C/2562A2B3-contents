#' Seawater Density according to UNESCO formula
#' @description  UNESCO (1981) Tenth report of the joint panel on
#' oceanographic tables and standards. UNESCO Technical
#' Papers in Marine Science, Paris, 25p
#'
#' @param S Salinity in psu (which is +/- equal to ppm)
#' @param T Temperature in degrees
#' @param p pressure in Bar
#' @examples
#' rho(S=35,T=0.5,p=10)
#' rho(8,10) #Should be 1005.94659
#' @export
rho = function(S,T,p=0) ifelse(p==0, rho_p0(S,T), rho_p0(S,T) / (1 - p/K(S,T,p)))

#' Standard  Mean Ocean Water (SMOW)
#' @param T Temperature in degrees Celsius
#' @export
rho_smow = function(T){
  a0 = 999.842594
  a1 = 6.793953 * 10^-2
  a2 = -9.095290 * 10^-3
  a3 = 1.001685 * 10^-4
  a4 = -1.120083 * 10^-6
  a5 = 6.536332 * 10^-9

  a0 + a1*T + a2*T^2 + a3*T^3 + a4*T^4 + a5*T^5
}

#' Density (rho) at normal atmospheric pressure (p = 0)
#' @param S Salinity in psu (~ppm)
#' @param T Temperature in degrees Celsius
#' @export
rho_p0 = function(S,T){
  b0 = 8.2449 * 10^-1
  b1 = -4.0899 * 10^-3
  b2 = 7.6438 * 10^-5
  b3 = -8.2467 * 10^-7
  b4 = 5.3875 * 10^-9

  c0 = -5.7246 * 10^-3
  c1 = 1.0227 * 10^-4
  c2 = -1.6546 * 10^-6
  d0 = 4.8314 * 10^-4

  B1 = b0 + b1*T + b2*T^2 + b3*T^3 + b4*T^4

  C1 = c0 + c1*T + c2*T^2

  rho_smow(T) + B1*S + C1*S^1.5 + d0*S^2
}

#' compressibility at p = 0
#' @param S Salinity in psu (~ppm)
#' @param T Temperature in degrees Celsius
#' @export
K_p0 = function(S, T){
  e0 = 19652.210
  e1 = 148.4206
  e2 = -2.327105
  e3 = 1.360477 * 10^-2
  e4 = -5.155288 * 10^-5

  K_w = e0 + e1*T + e2*T^2 + e3*T^3 + e4*T^4

  f0 = 54.6746
  f1 = -0.603459
  f2 = 1.099870 * 10^-2
  f3 = -6.167 * 10^-5

  F1 = f0 + f1*T + f2*T^2 + f3*T^3

  g0 = 7.944 * 10^-2
  g1 = 1.6483 * 10^-2
  g2 = -5.3009 * 10^-4

  G1 = g0 + g1*T + g2*T^2

  K_w + F1*S + G1*S^1.5
}

#' compressibility K
#' @param S Salinity in psu (~ppm)
#' @param T Temperature in degrees Celsius
#' @param p pressure in bar
#' @export
K = function(S,T,p){

  h0 = 3.2399
  h1 = 1.43713 * 10^-3
  h2 = 1.16092 * 10^-4
  h3 = -5.77905 * 10^-7

  i0 = 2.838 * 10^-3
  i1 = -1.0981 * 10^-5
  i2 = -1.6078 * 10^-6
  j0 = 1.91075 * 10^-4

  k0 = 8.50935 * 10^-5
  k1 = -6.12293 * 10^-6
  k2 = 5.2787 * 10^-8

  m0 = -9.9348 * 10^-7
  m1 = 2.0816 * 10^-8
  m2 = 9.1697 * 10^-10

  Bw = k0 + k1*T + k2*T^2
  B2 = Bw + (m0 + m1*T + m2*T^2)*S

  Aw = h0 + h1*T + h2*T^2 + h3*T^3
  A1 = Aw + (i0 + i1*T + i2*T^2) * S + j0*S^1.5
  K_p0(S,T) + A1*p + B2*p^2
}
