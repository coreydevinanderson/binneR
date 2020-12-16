# binneR

Functions for creating and plotting spatial correlograms in R.

This package was written to expand upon existing functionality for autocorrelation analysis available in other R packages (such as spdep and vegan), as well as to restore some of the functionality for correlogram analysis from the standalone software package "PASSaGE 2" (Rosenberg and Anderson 2011), which is no longer being supported. It is possible that the functionality from this package could be merged into an R implementation of the pyssage project (Python implementation of select functions from PASSaGE/PASSaGE 2). We are open to suggestions.  

At the moment there are seven functions available. The primary function is called binneR(), which allows more flexibility for binning pairs of locations into different types of distance classes for correlogram analysis. You can specify a certain number of bins containing an equal number of pairs in each bin (type = "ep"), bins based on custom distance classes (type = "cd"; where the user specifies the upper limits of each bin), or bins with a particular pair count in each bin (type = "pc"; where the user can also specify the number of bins).

For Moran's I or Geary's c correlograms, binneR() outputs an S3 object of type 'nblist'/'list', containing a list of weight lists (S4 class objects of class 'listw' from spdep) that can be passed to autocorrelogram_mc() or autocorrelogram(). For a Mantel correlogram, binneR() outputs an S3 class object of type 'mlist'/'list', containing a list of binary matrices that can be passed to mcorrelogram_mc(). For Moran's I or Geary's c correlograms, autocorrelgram_mc() and autocorrelogram() depend on functions from spdep (i.e. moran.mc & geary.mc or moran.test & geary.test, respectively). For Mantel correlograms, calculations and testing are accomplished via vegan::mantel. The output of these correlogram functions is an S3 class object of type 'spclist'/'list' containing the estimated autocorrelation coefficients and P-values (among other information), which can be used to plot correlograms. The function plot.spclist() can be used to plot correlograms directly (based on base::plot) or, if the user prefers, the information from the 'spclist' can be used to create their own custom plot (e.g. via base::plot or ggplot2).

The long term goal is to improve and expand upon the existing functionality to include omnidirectional and directional correlograms.

----

Workflow diagram:

-Create nblist or mlist via binneR(), then use plot.nblist() or plot.mlist() to explore the cumulative distribution of pairs counts for different binning schemes prior to calculating autocorrelation/correlation coefficients.

binner() -> plot.nblist() or plot.mlist()

-Create nblist or mlist via binneR(), then calculate and test significance of autocorrelation coefficients or standardized Mantel correlation coefficients, then plot.

binner() -> acorrelogram() or acorrelogram_mc() or mcorrelogram_mc() -> plot.spclist()  # create 

All code was written by:

Corey Devin Anderson, Ph.D.
Associate Professor
Valdosta State University

with contributions and inspiration from:

Michael S. Rosenberg
Associate Professor
Director of CBS
Virginia Commenwealth University


Send inquiries to:

Corey Devin Anderson
coreanderson@valdosta.edu
coreydevinanderson@gmail.com
229-249-2644
 
