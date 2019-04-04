# BiasedUrn

# Using the R package BiasedUrn to implement a permutation procedure to correct for confounders in case-control studies

## Introduction

In our recent paper [(Epstein, et al., 2012)](http://dx.doi.org/10.1016/j.ajhg.2012.06.004), we proposed to adjust case-control association tests (including tests of rare variation) for confounders using a permutation approach. The approach, which can adjust for an arbitrary number of continuous and categorical covariates, can be implemented using a modified version of an open source R package called [BiasedUrn](http://cran.r-project.org/web/packages/BiasedUrn/index.html) authored and maintained at CRAN by [Agner Fog](http://www.agner.org/). This page describes how to modify and install this package and also provides sample code for implementing the approach.

## The R base system

R is a widely-used, free and open source software environment for statistical computing and graphics. The most recent version of R can be downloaded from the [Comprehensive R Archive Network (CRAN)](http://cran.r-project.org/). CRAN provides precompiled binary versions of R for Windows, MacOS, and select Linux distributions that are likely sufficient for many users' needs. Users can also install R from source code; however this may require a significant amount of effort. For specific details on how to compile, install, and manage R and R-packages, refer to the manual <cite>[R Installation and Administration](http://cran.r-project.org/doc/manuals/R-admin.html)</cite>, which is available from the [CRAN documentation site](http://cran.r-project.org/manuals.html).

## Building the BiasedUrn package

While a precompiled version of the BiasedUrn library is available on CRAN, this precompiled version cannot be used for the sampling performed in our AJHG paper because it only allows for a maximum of 32 subjects (see our paper for more details). Consequently, to increase the sample size to values anticipated for case-control association studies, one must download the source code for BiasedUrn, make a minor change to the source code, and then recompile and install the modified executable for analysis. We describe how to perform these tasks for different operating systems below.

### Step 1: Downloading the package source

To obtain the BiasedUrn package source code, go to the [repository for the package on CRAN](http://cran.r-project.org/web/packages/BiasedUrn/index.html) and download the source file BiasedUrn_1.04.tar.gz as highlighted in Figure 1.

![alt text](http://genetics.emory.edu/labs/epstein/software/BiasedUrn/CRAN-burn-page.png "Logo Title Text 1")


<figcaption>Figure 1. The BiasedUrn package page at CRAN. The package source link is highlighted here.</figcaption>


### Step 2: Modifying, compiling, and installing the BiasedUrn Package

Each operating system uses a different set of developer tools to build R packages from source code; however, the basic steps are the same for each operating system:

*   modify the <tt>MAXCOLORS</tt> constant in the <tt>Makevars</tt> file found within the package source code
*   run the `R CMD check` command to verify the modified package
*   run the `R CMD build` command to create an installable package
*   run the `R CMD INSTALL` command to install the modified package

We provide OS-specific instructions for modifying and installing the source code below:

*   [Linux](burn-install-linux.md)
*   [Mac OS](burn-install-macos.md)
*   [Windows](burn-install-windows.md)

## Using modified BiasedUrn to create permuted datasets

Once the modified version of BiasedUrn is properly installed, the procedure can be used to generate permuted case-control datasets that are adjusted for confounders. Please see our [sample R code](burn-example.md) for an example that uses the procedure.

## Questions and technical support

For questions or concerns with the BiasedUrn package, please contact [Richard Duncan](mailto:rduncan@emory.edu) and [Michael Epstein](mailto:mpepste@emory.edu).  
We appreciate any feedback you have with our site and instructions. ![wordcloud-biased-urn-permutation-sampling_ajhg-2012](http://genetics.emory.edu/labs/epstein/software/BiasedUrn/wordcloud-biased-urn-permutation-sampling_ajhg-2012.png)

[Epstein software](http://genetics.emory.edu/labs/epstein/software/index.html) | [Human Genetics](http://genetics.emory.edu/) | [School of Medicine](http://www.med.emory.edu/) | [Emory University](http://www.emory.edu/)
