---
title: "Fitbit Heart Hangover (W241)"
author: "Paul Durkin"
date: "April 17, 2018"
output: pdf_document
---



# Pilot analysis

Interesting things here:
* Initial analysis just doing the delta from the previous day shows a statistically significant intercept of approximately -0.5 indicating that on the days of no alcohol effect there is a decline in heart rate.  This is interesting because it would imply a continuously decreasing heart rate which we know is not true.  The cause of this is twofold
1. This was my heart rate in January/February.  January saw a "normalization" of my heart rate as here was a huge increase in December due to lack of exercise at the end of term followed by a sedentary Christmas vacation.
2. This naively ignores the recovery from a previous effect.  If we have an effect one day then the next day there is a decline as it normalizes again.  
  
There are two fixes for this
1. I take a subset of the data from the point (21st entry) where my heart rate dropped under 60 again
2. Measure the change from the last control day rather than simply the previous day.  This is the last day that had no treatment effect.

The analysis is in the following table.  It shows that when we use the previous control that the intercept is no longer statistically significant.



```
## 
## ===================================================================================
##                                           Dependent variable:                      
##                     ---------------------------------------------------------------
##                                Change.HR              Change.HR.Previous.Control   
##                           (1)             (2)             (3)             (4)      
## -----------------------------------------------------------------------------------
## Treatment.Yesterday    1.945***        1.750***        1.719***         1.361**    
##                         (0.404)         (0.613)         (0.398)         (0.588)    
##                                                                                    
## Constant               -0.491***        -0.500          -0.264          -0.111     
##                         (0.190)         (0.426)         (0.177)         (0.389)    
##                                                                                    
## -----------------------------------------------------------------------------------
## Observations              64              26              64              26       
## R2                       0.239           0.215           0.217           0.161     
## Adjusted R2              0.226           0.182           0.204           0.127     
## Residual Std. Error 1.332 (df = 62) 1.607 (df = 24) 1.251 (df = 62) 1.490 (df = 24)
## ===================================================================================
## Note:                                                   *p<0.1; **p<0.05; ***p<0.01
```

This shows the decline of my RHR over January and the stabilization at the end.

![](AnalysisFitbitW241_files/figure-latex/unnamed-chunk-2-1.pdf)<!-- --> 

## Analysis of the main data

### Simple regression
First things first, is there an effect without including any covariates




```
## 
## ============================================================================================================================================================================================
##                                                                                                       Dependent variable:                                                                   
##                                     --------------------------------------------------------------------------------------------------------------------------------------------------------
##                                                                                          Change.in.Fitbit.HR.from.previous.control.day                                                      
##                                           (1)              (2)              (3)              (4)              (5)              (6)              (7)              (8)              (9)       
## --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Volume.Pure.Alcohol.in.previous.day 0.024** (0.008)  0.023** (0.009)  0.023** (0.008)  0.024** (0.008)  0.024** (0.008)  0.023** (0.008)  0.024** (0.008)  0.024** (0.008)  0.024** (0.009) 
## Female                                                -0.034 (0.358)                                                                                        0.302 (0.415)    -1.828 (2.863) 
## Weight.LBS                                                             0.008 (0.006)                                                                        0.012 (0.009)    0.020 (0.019)  
## age                                                                                     0.019 (0.021)                                                       0.001 (0.026)    0.281 (0.410)  
## BMI                                                                                                      0.102 (0.054)                                                                      
## exercise                                                                                                                  0.322 (0.383)                                      1.065 (1.009)  
## CV.Meds                                                                                                                                                                      -1.442 (1.758) 
## height.inches                                                                                                                                                                -0.632 (0.731) 
## PSTPlus                                                                                                                                    0.002 (0.060)                     -0.300 (0.507) 
## Constant                             -0.210 (0.215)   -0.193 (0.309)   -1.435 (0.863)   -0.878 (0.784)  -2.528* (1.232)   -0.343 (0.274)   -0.222 (0.545)   -2.149 (1.167)  32.161 (40.515) 
## --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Observations                              125              125              125              125              125              125              125              125              125       
## R2                                       0.136            0.136            0.143            0.140            0.147            0.141            0.136            0.146            0.188      
## Adjusted R2                              0.129            0.122            0.129            0.126            0.133            0.127            0.122            0.118            0.131      
## Residual Std. Error                 2.099 (df = 123) 2.108 (df = 122) 2.099 (df = 122) 2.104 (df = 122) 2.095 (df = 122) 2.102 (df = 122) 2.108 (df = 122) 2.113 (df = 120) 2.097 (df = 116)
## ============================================================================================================================================================================================
## Note:                                                                                                                                                          *p<0.05; **p<0.01; ***p<0.001
```


```
## 
## Manual Regressions Comparison
## ============================================================================================================================================================================================
##                                                                                                       Dependent variable:                                                                   
##                                     --------------------------------------------------------------------------------------------------------------------------------------------------------
##                                                                                          Change.in.manual.HR.from.previous.control.day                                                      
##                                           (1)              (2)              (3)              (4)              (5)              (6)              (7)              (8)              (9)       
## --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Volume.Pure.Alcohol.in.previous.day     0.034**          0.034**          0.033**          0.033**          0.033**          0.034**          0.034**          0.033**          0.037***    
##                                         (0.011)          (0.011)          (0.011)          (0.011)          (0.011)          (0.011)          (0.011)          (0.012)          (0.011)     
##                                                                                                                                                                                             
## Female                                                    0.049                                                                                                 0.0004           -1.158     
##                                                          (0.506)                                                                                               (0.739)          (0.903)     
##                                                                                                                                                                                             
## Weight.LBS                                                                 -0.006                                                                               -0.005           0.011      
##                                                                           (0.008)                                                                              (0.012)          (0.017)     
##                                                                                                                                                                                             
## age                                                                                         -0.012                                                              -0.008           0.0004     
##                                                                                            (0.022)                                                             (0.033)          (0.042)     
##                                                                                                                                                                                             
## BMI                                                                                                          -0.028                                                                         
##                                                                                                             (0.063)                                                                         
##                                                                                                                                                                                             
## exercise                                                                                                                      0.855                                              1.747*     
##                                                                                                                              (0.511)                                            (0.789)     
##                                                                                                                                                                                             
## CV.Meds                                                                                                                                                                          -2.511     
##                                                                                                                                                                                 (1.519)     
##                                                                                                                                                                                             
## height.inches                                                                                                                                                                    -0.239     
##                                                                                                                                                                                 (0.261)     
##                                                                                                                                                                                             
## PSTPlus                                                                                                                                        -0.025                            0.152      
##                                                                                                                                               (0.069)                           (0.118)     
##                                                                                                                                                                                             
## Constant                                 -0.101           -0.125           0.797            0.362            0.591            -0.573           0.065            1.000            12.947     
##                                         (0.278)          (0.387)          (1.331)          (0.932)          (1.584)          (0.410)          (0.534)          (1.536)          (16.769)    
##                                                                                                                                                                                             
## --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Observations                              149              149              149              149              149              149              149              149              149       
## R2                                       0.112            0.112            0.115            0.113            0.113            0.129            0.113            0.115            0.175      
## Adjusted R2                              0.106            0.100            0.103            0.101            0.101            0.117            0.101            0.091            0.127      
## Residual Std. Error                 3.086 (df = 147) 3.097 (df = 146) 3.093 (df = 146) 3.095 (df = 146) 3.095 (df = 146) 3.067 (df = 146) 3.095 (df = 146) 3.113 (df = 144) 3.049 (df = 140)
## ============================================================================================================================================================================================
## Note:                                                                                                                                                          *p<0.05; **p<0.01; ***p<0.001
```

Both of these show a statistically significant result which immediately seems to lean towards the hypothesis that the effect is real.

