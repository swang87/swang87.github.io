---
title: Graphical Product Partition Models
subtitle: With an application in image processing
author: Xiaofei (Susan) Wang
job: PhD Candidate, Yale University 
email: xiaofei.wang@yale.edu
website: http://xiaofei-wang.com
collab: John W. Emerson
collab-website: http://www.stat.yale.edu/~jay
widgets: [mathjax, bootstrap]
url:
  lib   : libraries
  assets: assets
mode: selfcontained

--- .segue .dark

## Overview



--- 

## Classical Change Point Problem ##
Data: $y_1,\dots, y_n$, where $y_i \sim N(\theta_i, \sigma^2)$.
### Example 1

![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2.png) 

---

## Classical Change Point Problem ##
### Example 2

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3.png) 

--- 

## Classical Change Point Problem ##
### Example 2

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4.png) 

--- 

## Literature Survey ##
- Barry and Hartigan (1993), Erdman and Emerson (2007, 2008) - univariate change points via `library(bcp)`
- Barry and Hartigan (1994) - univariate change points on a grid
- Bai and Perron (2003), Zeileis, et al. (2001) - regression change points via `library(strucchange)`
- Muggeo (2003) - regression change points via `library(segmented)`
- Olshen, et al. (2004) - univariate change points using circular binary segmentation
- Fearnhead (2005) - Bayesian regression change points
- Loschi, et al. (2010) - Bayesian regression change points
- Killick and Eckley (2011) - univariate mean or variance change points via `library(changepoint)`
- Ross (2012) - distributional univariate change points via `library(cpm)`
- Matteson and James (2013) - multivariate change points via `library(ecp)`
- ... and others

--- &twocol

## Bayesian Change Point Analysis ##
### Barry & Hartigan (1993): A Product Partition Model

***left
<div style="font-size: 110%;">  
Partition $\rho = (S_1,\dots, S_b)$
$$y_{i:i\in S}\sim N(\theta_S, \sigma^2)$$
$$ \theta_S|\mu_0, \sigma_0^2 \sim N\left(\mu_0, \frac{\sigma_0^2}{n_S}\right)$$
<div style="color: red;">
$$f(\rho|p) = p^{b-1} (1-p)^{n-b}$$
</div>
</div>

***right
<div style="font-size: 110%;">  
$$\mu_0 \sim U(-\infty, \infty)$$
$$\pi(\sigma^2) \propto \frac{1}{\sigma^2}\;\;\;\;\sigma^2\in(0,\infty)$$
$$\pi(p) = \frac{1}{p_0}\;\;\;\;p\in (0,p_0)$$
$$\pi(w) = \frac{1}{w_0}\;\;\;\;w\in(0,w_0)$$
</div>

---

## Product Partition Models (PPMs) ##

### Hartigan (1990):
<q>
Product partition models assume that observations in different components of a random partition of the data are independent given the partition.</q>
<div class="build"> 
<div class="alert alert-info">
i.e. $y_i$ in block $S_1$ is independent of $y_j$ in $S_2$ given partition $\rho$ and the other parameters.
</div>
</div>

--- &twocol

## Bayesian Change Point Analysis ##
- Univariate change point analysis (Barry & Hartigan 1992)
- Implemented by Erdman & Emerson (2007, 2008) in `library(bcp)`

*** left 
### Example 1 (revisited)
![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5.png) 


*** right
### Example 1 (`bcp` output)
![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6.png) 



--- .segue .dark

## Extensions

--- &twocol

## Simple linear regression ##

*** left 
### Example 3
![plot of chunk unnamed-chunk-7](figure/unnamed-chunk-7.png) 


*** right
### Example 3 (posterior output)
![plot of chunk unnamed-chunk-8](figure/unnamed-chunk-8.png) 


--- &twocol

## Multivariate change point

*** left 

### Example 4

![plot of chunk unnamed-chunk-9](figure/unnamed-chunk-9.png) 


*** right

### Example 4 (posterior output)

![plot of chunk unnamed-chunk-10](figure/unnamed-chunk-10.png) 



--- .segue .dark

## Moving to a Grid

--- &twocol

## Change Points on a Grid##
### Barry and Hartigan (1994)
*** left 

### Example 5

![plot of chunk unnamed-chunk-11](figure/unnamed-chunk-11.png) 


*** right

### Example 5 (posterior means)

![plot of chunk unnamed-chunk-12](figure/unnamed-chunk-12.png) 


--- 
## Change Points on a Grid ##
What does it mean to have a change point on a grid?

### In 1 dimension

![plot of chunk unnamed-chunk-13](figure/unnamed-chunk-13.png) 


--- 

## Change Points on a Grid ##
What does it mean to have a change point on a grid?

### In 2 dimensions

![plot of chunk unnamed-chunk-14](figure/unnamed-chunk-14.png) 


---
## Change Points on a Grid ##
The model only differs in the prior.

>  - Boundary length $l(\rho)$
<div style="font-size: 150%;">  
  $$ f(\rho)\propto \alpha^{l(\rho)} \;\;\;\;\; \alpha\in(0,1)$$
</div>
>  - Small $\alpha$ encourages shorter boundaries
>  - Results are very sensitive to choice of $\alpha$ 

However, the MCMC implementation is much more complicated.

--- &twocol

## Application
### Image Restoration

*** left
### Example 6


<img src="pictures/house_ns25.jpg" width=350>

*** right
### Example 6 (posterior means)


<img src="pictures/house_ns-25.jpg" width=350>

--- &twocol

## Application: Multivariate
### Image Restoration

*** left
### Example 7 (RGB channels)


<img src="pictures/house-orig-multi-0.1.jpg" width=350>

*** right
### Example 7 (posterior means)


<img src="pictures/house-out-multi-0.1.jpg" width=350>

---

## Application: Multivariate
### Ad-Hoc Image Segmentation (via k-means)

### Example 7 (segments)


<div class="row-container">
  <div class="span3">
<img src="pictures/tmp6.jpg" width=200>
  <img src="pictures/tmp1.jpg" width=200>
  </div>
 <div class="span3">
<img src="pictures/tmp4.jpg" width=200>
  <img src="pictures/tmp2.jpg" width=200>
  </div>
  <div class="span3">
<img src="pictures/tmp5.jpg" width=200>
  <img src="pictures/tmp3.jpg" width=200>
  </div>
</div>

--- &twocol

## From Grid to Graph

*** left
### Example 8

![plot of chunk unnamed-chunk-20](figure/unnamed-chunk-20.png) 


*** right
### Example 8 (change point output)

![plot of chunk unnamed-chunk-21](figure/unnamed-chunk-21.png) 



--- .segue .dark

## Future Directions

--- 

## Next Steps
1. Refining and improving the graphical change point method for both the univariate and multivariate cases.
2. Extending the graphical change point method to fitting regressions.

--- .segue .dark

## Thank You ##

--- 

## Acknowledgements
I would like to thank my advisors Jay Emerson and Joseph Chang for their 
support and neverending wealth of ideas. Also, I would also like to thank my academic
grandfather, John Hartigan, for pioneering the concept of product partition models.

---

## References

- Barry, Daniel, and John A. Hartigan. "A Bayesian analysis for change point problems." Journal of the American Statistical Association 88.421 (1993): 309-319.
- Hartigan, John A. "Partition models." Communications in Statistics-Theory and Methods 19.8 (1990): 2745-2756.
- Barry D, Hartigan JA. A product partition model for image restoration. In New Directions in Statistical Data Analysis and Robustness, MorgenthalerS (ed.). Birkhäuser: Basel, 1994.
- Erdman, Chandra, and John W. Emerson. "bcp: An R package for performing a Bayesian analysis of change point problems." Journal of Statistical Software 23.3 (2007): 1-13.
- Erdman, Chandra, and John W. Emerson. "A fast Bayesian change point analysis for the segmentation of microarray data." Bioinformatics 24.19 (2008): 2143-2148.
- Matteson, David S., and Nicholas A. James. "A nonparametric approach for multiple change point analysis of multivariate data." arXiv preprint arXiv:1306.4933 (2013).
- Bai, Jushan, and Pierre Perron. "Computation and analysis of multiple structural change models." Journal of Applied Econometrics 18.1 (2003): 1-22.

---

## References
- Loschi, Rosangela H., Jeanne G. Pontel, and Frederico RB Cruz. "Multiple change-point analysis for linear regression models." Chilean Journal of Statistics 1 (2010): 93-112.
- Fearnhead, Paul. "Exact Bayesian curve fitting and signal segmentation." Signal Processing, IEEE Transactions on 53.6 (2005): 2160-2166.
- Killick, Rebecca, and Idris A. Eckley. "Changepoint: an R package for changepoint analysis." Lancaster University (2011).
- Ross, Gordon J. "Parametric and Nonparametric Sequential Change Detection in R: The cpm package." Journal of Statistical Software, 2012.
- Hegarty, Avril, and Daniel Barry. "Bayesian disease mapping using product partition models." Statistics in medicine 27.19 (2008): 3868-3893.
- Muggeo, Vito MR. "Estimating regression models with unknown break‐points." Statistics in medicine 22.19 (2003): 3055-3071.
- Olshen, Adam B., et al. "Circular binary segmentation for the analysis of array‐based DNA copy number data." Biostatistics 5.4 (2004): 557-572.

---

## References
- Zeileis, Achim, et al. "strucchange. An R package for testing for structural change in linear regression models." (2001).
