#' Computes ka
#'
#' @param para [list] A list containing all the model parameters (\url{../doc/parameters.html})
#' @param misc [list] A list with misc parameters, containing at least the soundspeed of the surrounding fluid cw
#' @param app TRUE or FALSE, defines if the function is used within a shiny app or not. If \code{app==TRUE} the progressbar inside the app will be updated.
#' @return list of \code{ka}, the wavelength \code{k * } the width \code{a}; f the square-root of the orientation aveaged scattering cross-section
#' @examples
#' #Get filename of the parameters file
#' fname <- paste0(system.file(package = "ZooScatR"),"/extdata/configs/config_0.dat")
#' #Read in teh parameter
#' para = read_para(fname)
#' #Create list with soundspeed info
#' misc <- list()
#' misc$cw <- 1500
#' DWBAscat2(para,misc)
#' @export

DWBAscat2 <- function(para, misc, app=FALSE){
  if(exists("status")==FALSE){status=list()}
  status$stop = 0
  #print(para$shape$prof_name)
  eps<-2.2204e-16
  # shape parameters
  L_a = para$shape$L_a

  # simulation parameter
  n = length(misc$ka)				# N of ka point
  n_int = para$simu$ni		# N of integration points

  ang = misc$ang 		# different incident angle
  m = length(ang)
  th = ang*(pi/180) #degrees to radians

  ka0 = misc$ka

  # construct inhomogeneous g ang h profile (physical parameters)

  if(para$phy$body_ih == FALSE){
    g = para$phy$g0 * matrix(1, n_int, 1)
    h = para$phy$h0 * matrix(1, n_int, 1)
    para$phy$g = g
    para$phy$h = h
  }else{
    if(app==FALSE){
      igh <- inhom_gh(para)
      para$phy$g <- igh$g
      para$phy$h <- igh$h
    }
    g=as.matrix(para$phy$g)
    h=as.matrix(para$phy$h)
  }

  Cb = (1- g * h * h) / (g * h * h) - (g-1) / g

  # construct postion vectors
  bp <- buildpos(para)
  r_pos = as.matrix(bp$r_pos)
  th_tilt = bp$th_tilt
  dr = bp$dr
  gamma_t = bp$gamma_t
  taper = bp$taper
  xp = bp$x
  zp = bp$z

  # construct other Matrices
  X1 = as.matrix(ka0) %*% t(taper)
  Tmp = t(h[,matrix(1, 1, n)])
  X2 = X1 / Tmp
  th <- (as.matrix(th))
  th_tilt <- as.matrix(th_tilt)
  Dtheta = t(th_tilt[,matrix(1,1,m)]) - th[,matrix(1, 1, n_int)]

  Cos_dtheta = abs(cos(Dtheta))   # choose different local coordinates to
  # avoid negtive argument of Bessel function
  Gamma_t = t(as.matrix(gamma_t)[,matrix(1, 1, m)])
  Theta = th[,matrix(1, 1,n_int)]
  Dgamma = Gamma_t-Theta
  Cos_dgamma = cos(Dgamma)
  ka0 = as.matrix(ka0)
  term0 = (L_a * ka0) %*% t(r_pos/h)
  term1 = h * h * Cb * as.matrix(dr) /4
  Jarr = 1:m					  # angle index for checking purpose
  f=matrix(0,length(ka0), length(Jarr))

  for( J in 1:length(Jarr)){
    if(app==TRUE){
      incProgress(0.85/length(Jarr), detail = paste("Running model -", J/length(Jarr)*100,"%"))
      #print(J)
    }
    # angle loop
    # disp(sprintf(' j = #g, stop =#g',J,status.stop))
    if(status$stop == 0){
      j = Jarr[J]
      cos_dtheta = as.matrix(Cos_dtheta[j,])
      Cos_th = t(cos_dtheta[,t(matrix(1, 1, n))])
      cos_dgamma = as.matrix(Cos_dgamma[j,])
      Cos_gamma = t(cos_dgamma[,matrix(1, n,1)])
      Arg = (2 * X2 * (Cos_th) + eps)
      J1x = as.matrix(besselJ(Arg,1)) / Arg
      EXP = exp(1i * term0 * Cos_gamma)
      term2 = (X2*X2) *  J1x * EXP
      f[,j] = term2 %*% term1 + eps
    }else{
      f=0
      return()
  }
  }
  return(list(ka=ka0,ang=ang,f=f, shplot = bp$plot))
}

