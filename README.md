# PCA_Geomorfometria_ESP
#carpeta
setwd("~/Análisis de Tesis en Rstudio y SAGA GIS/Variables/Georfometria R_SAGA GIS/Prueba_19_02_21/Variables de SAGA GIS")
library(raster)
#Unificar archivos
list.files(pattern = ".sgrd")
{
 [1] "Analytical Hillshading.sgrd"               "Aspect.sgrd"                              
 [3] "Channel Network Base Level.sgrd"           "Closed Depressions.sgrd"                  
 [5] "Convergence Index.sgrd"                    "Cross-Sectional Curvature.sgrd"           
 [7] "Flow Accumulation.sgrd"                    "Longitudinal Curvature.sgrd"              
 [9] "LS Factor.sgrd"                            "Relative Slope Position.sgrd"             
[11] "Slope.sgrd"                                "Topographic Wetness Index.sgrd"           
[13] "Valley Depth.sgrd"                         "Vertical Distance to Channel Network.sgrd"
}

top <- stack(list.files(pattern = ".sgrd"), native=TRUE)

top
class      : RasterStack 
dimensions : 1044, 1656, 1728864, 15  (nrow, ncol, ncell, nlayers)
resolution : 0.008333333, 0.008333333  (x, y)
extent     : -9.4, 4.4, 35.2, 43.9  (xmin, xmax, ymin, ymax)
crs        : NA 
names      : Analytical.Hillshading, Aspect, Channel.Network.Base.Level, Closed.Depressions, Convergence.Index, Cross.Sectional.Curvature, Flow.Accumulation, Longitudinal.Curvature, LS.Factor, Relative.Slope.Position, Slope, Topographic.Wetness.Index, Valley.Depth, Vertical.//el.Network,  DEM 
min values :                      ?,      ?,                          ?,                  ?,                 ?,                         ?,                 ?,                      ?,         ?,                       ?,     ?,                         ?,            ?,                     ?,   -1 
max values :                      ?,      ?,                          ?,                  ?,                 ?,                         ?,                 ?,                      ?,         ?,                       ?,     ?,                         ?,            ?,                     ?, 2725 

names(top)
 [1] "Analytical.Hillshading"               "Aspect"                              
 [3] "Channel.Network.Base.Level"           "Closed.Depressions"                  
 [5] "Convergence.Index"                    "Cross.Sectional.Curvature"           
 [7] "Flow.Accumulation"                    "Longitudinal.Curvature"              
 [9] "LS.Factor"                            "Relative.Slope.Position"             
[11] "Slope"                                "Topographic.Wetness.Index"           
[13] "Valley.Depth"                         "Vertical.Distance.to.Channel.Network"
[15] "DEM"     
#cargar el DEM
dem <- raster("~/Análisis de Tesis en Rstudio y SAGA GIS/Variables/Georfometria R_SAGA GIS/Prueba_19_02_21/DEM.tif")
#Unificar
top1 <- stack(top, dem)
#carga, NO VOLVER A CORRER, YA ESTA INSTALADO
#install.packages("RStoolbox")
library(RStoolbox)
#PCA
rpc <- rasterPCA(top1, spca=TRUE)
 names(rpc)
[1] "call"  "model" "map"  
> plot(rpc$map)
> 



summary(rpc$model) 
loadings(rpc$model)
