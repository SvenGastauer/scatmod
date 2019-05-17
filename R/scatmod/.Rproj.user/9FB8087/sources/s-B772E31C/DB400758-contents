#' @title rho_c
#' @description Radius of curvature
#' @param x x coordinates
#' @param y y coordinates
#' @export

rho_c = function(x,y){
  #get center of mass
  mx <- mean(x); my<- mean(y)
  X <- x-mx; Y=y-my
  dx2 <- mean(X^2); dy2 <- mean(Y^2)

  RHS <- (x^2 - dx2 + Y^2 - dy2)/2

  M <- c(X,Y)

  t = M/RHS

  a0 <- t[1]; b0 <- t[2]

  r <- sqrt(dx2 + dy2 + a0^2 + b0^2)

  a <- a0+mx

  b = b0+my

}
