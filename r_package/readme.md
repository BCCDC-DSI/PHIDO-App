
# Technical introduction

PHIDO fits a set of generalized additive models on the input data on case counts and outputs an estimate of the expected count "fitted counts". To reduce the effects of outliers on the output estimates, PHIDO uses an ***iterative down-weighting scheme***.


## Example of input data

Figure 1:
![image](https://github.com/user-attachments/assets/c63f0e71-71c4-4933-9142-0292eea34883)

## Sample code snippet

Relating the code below to Figure 1:
- ```input$x``` is a vector of ***date*** in Figure 1
- ```input$y``` is a vector of ***count*** in Figure 1

```
install.packages( c("gam", "robustbase") )
install.packages( "//phsabc.ehcnet.ca/root/BCCDC/Groups/Analytics_Resources/Coding/R/Library/PHIDO_0.2.0.tar.gz", repos = NULL )

# renv users:
install.packages( pkgs = "//phsabc.ehcnet.ca/root/BCCDC/Groups/Analytics_Resources/Coding/R/Library/PHIDO_0.2.0.tar.gz",
  lib = "//phsabc.ehcnet.ca/root/BCCDC/Groups/<project_folder>/renv/library/<which_R_ver>/x86_64-w64-mingw32",
  INSTALL_opts = '--no-lock',
  repos = NULL)

library("PHIDO")
library("dplyr")
library("ggplot2")

data(package = "PHIDO")

input <- PHIDO::high_count_varied

output <- mainPHIDO(x = input$x,
 y = input$y, 
HighP = 0.001,
 MidP = 0.01,
 LowP = 0.05)

tail( select(output, x, y, AlertPeriodStart, AlertPeriodEnd, AlertScorePvalue) )
```
Source: [User Guide](https://healthbc.sharepoint.com/sites/BCCDCDataAnalyticsServicePHSA/_layouts/15/download.aspx?SourceUrl=/sites/BCCDCDataAnalyticsServicePHSA/Epidemiological%20Methods/PHIDO%20user%20manual%20V2%20for%20sharepoint.pdf)


## Sample outputs & visualization

After plotting the outputs (```fitted_counts```), one would get a trendline like this:

![image](https://github.com/user-attachments/assets/146ba070-048d-442a-b5dd-f5c2cf5768f3)

## Mathematics behind PHIDO 

PHIDO expresses the mean function $\lambda(t)$ as:
$log( \lambda(t) ) = a + \beta t + f(t) + c(t)$

- Where the last 2 terms are ***non-parameteric*** and are fitted using ***locally estimated scatter plot smoothing***
- $f(t)$ cpatures long-term trend; it is excluded if there are less than 10 non-zero counts
- $c(t)$ captures seasonal trend
- The span for $c(t)$ is always 1, all data points
- The span for $f(t)$ is the smallest section with at least 10 non-zero counts and span more than 2 years of data

## Iterative down-weighting scheme (IDWS) 

By default, PHIDO runs a maximum of 20 iterations in the IDWS, where counts of zeros are all given weights of 1.0 initially. 

Next, the counts are sorted in ascending order^ and weights for each case count are adjusted one-by-one in this order.
For instance, if a jump happens, e.g. $Y_k>2\*Y_{k-1}$ (or $Y_k > 2$ and $Y_{k-1}$, then the weight for count $o+1$ is computed as:
      $w_{k} = 2*Y_{k-1} / Y_{k}$. More details on the heuristics are presented in [Lee's thesis](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwjcserk-f-IAxVICTQIHYlrES4QFnoECBUQAQ&url=https%3A%2F%2Fopen.library.ubc.ca%2Fmedia%2Fstream%2Fpdf%2F24%2F1.0380711%2F4&usg=AOvVaw1XUjdEcZI-gdNSnpSMRPx2&opi=89978449). 

The pseudo-algorithm looks like:

```
w <- calc_init_weights( input$y )

for (itn in 1:20){
  m <- gam(model,family=quasi(log,mu), weights=w )
  sigma_sqr  <- dispersion_fn( ... )
  residuals <- calc_residuals( sigma_sqr, model )

  residuals <- residuals / sqrt( sigma + 1e-20 )
  cond_distr <- calc_cond_distr( input$y, sigma_sqr )

  P1 <- 1 - probBinomialThruBeta_fn( ... )
  P2 <- pnorm( residuals ) - 1
  P3 <- pmax( 0.9, P1*P2 )
  w <- w*(1-P3)*10
}

```

<br>
^Asscending order would sort [0,0,22,0,0,0,0,1,0] to [0,0,0,0,0,0,0,1,22]

## Recap

- Trends from non-parametric estimations will be disabled under any of the following conditions:
    - Less than 2 years of training data
    - Less than 10 non-zero counts per year
    - Less than 10 non-zero counts in the entire data

 
[Return to home](../..)

