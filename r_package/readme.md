
# Input

![image](https://github.com/user-attachments/assets/c63f0e71-71c4-4933-9142-0292eea34883)

## Sample code snippet

```
install.packages( c("gam", "robustbase") )
install.packages( "//phsabc.ehcnet.ca/root/BCCDC/Groups/Analytics_Resources/Coding/R/Library/PHIDO_0.2.0.tar.gz", repos = NULL )

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
```
Source: [User Guide](https://healthbc.sharepoint.com/sites/BCCDCDataAnalyticsServicePHSA/_layouts/15/download.aspx?SourceUrl=/sites/BCCDCDataAnalyticsServicePHSA/Epidemiological%20Methods/PHIDO%20user%20manual%20V2%20for%20sharepoint.pdf)


# Output



# Notes:

Seasonal trends not feasible if any of below:
- Less than 2 years of training data
- Less than 10 non-zero counts per year
- Less than 10 non-zero counts in the entire data


Non-parametric portions fitted using locally estimated scatter plot smoothing

weighted generalized additive models
