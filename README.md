# binneR

Functions for creating and plotting spatial correlograms in R.

This package was written to expand upon existing functionality for autocorrelation analysis available in other R packages (such as spdep and vegan), as well as to restore some of the functionality for correlogram analysis from the standalone software package "PASSaGE 2" (Rosenberg and Anderson 2011), which is no longer being supported. It is possible that the functionality from this package could be merged into an R implementation of the pyssage project (Python implementation of select functions from PASSaGE/PASSaGE 2). We are open to suggestions.  

At the moment there are seven functions available. The primary function is called binneR(), which allows more flexibility for binning pairs of locations into different types of distance classes for correlogram analysis. You can specify a certain number of bins containing an equal number of pairs in each bin (type = "ep"), bins based on custom distance classes (type = "cd"; where the user specifies the upper limits of each bin), or bins with a particular pair count in each bin (type = "pc"; where the user can also specify the number of bins).

For Moran's I or Geary's c correlograms, binneR() outputs an S3 object of type 'nblist'/'list', containing a list of weight lists (S4 class objects of class 'listw' from spdep) that can be passed to autocorrelogram_mc() or autocorrelogram(). For a Mantel correlogram, binneR() outputs an S3 class object of type 'mlist'/'list', containing a list of binary matrices that can be passed to mcorrelogram_mc(). For Moran's I or Geary's c correlograms, autocorrelgram_mc() and autocorrelogram() depend on functions from spdep (i.e. moran.mc & geary.mc or moran.test & geary.test, respectively). For Mantel correlograms, calculations and testing are accomplished via vegan::mantel. The output of these correlogram functions is an S3 class object of type 'spclist'/'list' containing the estimated autocorrelation coefficients and P-values (among other information), which can be used to plot correlograms. The function plot.spclist() can be used to plot correlograms directly (based on base::plot) or, if the user prefers, the information from the 'spclist' can be used to create their own custom plot (e.g. via base::plot or ggplot2).

The long term goal is to improve and expand upon the existing functionality to include omnidirectional and directional correlograms.

----

Current workflow diagram:

-Create 'nblist' or 'mlist' via binneR(), then use plot.nblist() or plot.mlist() to explore the cumulative distribution of pairs counts for different binning schemes prior to calculating autocorrelation/correlation coefficients.

binner() -> plot.nblist() or plot.mlist()

-Create 'nblist' or 'mlist' via binneR(), then calculate and test significance of autocorrelation coefficients or standardized Mantel correlation coefficients (output is an 'spclist'), then pass to plot.spclist() to create a correlogram or use information contained in 'spclist' to create your own correlogram with the graphing utility of your choice.

binner() -> acorrelogram() or acorrelogram_mc() or mcorrelogram_mc() -> plot.spclist()

--

binner() requires a symmetrical pairwise distance matrix from which to create the bins for the 'nblist' or 'mlist'.

plot.nblist() requires a 'nblist' from binneR(); plot.mlist() requires an 'mlist' from binneR().

acorrelogram() and acorrelogram() require a 'nblist' from binneR() and a data vector (of length n equal to the number of locations used to create the 'nblist').

mcorrelogram_mc() requires an 'mlist' from binneR() and data matrix with the same dimensions as the geographic distance matrix.

plot.spclist() requires an 'spclist' from acorrelogram() or acorrelogram_mc() or mcorrelogram_mc()

--

Test data are available in the "available data" folder, along with a file containing R code to process the data for use with binneR.

We encourage you to also try your own data as we continue to test these functions in preparation for submission to CRAN.


---

All code was written by:

Corey Devin Anderson, Ph.D., while a Associate Professor at Valdosta State University during a sabbatical at VCU.
Corey is now a Geospatial Statistician Lead on the GRASP-GEAR team at the CDC/ATSDR via DRT Strategies.

Contributions and inspiration from:

Michael S. Rosenberg
Professor
Director of CBS
Virginia Commenwealth University

Special thanks to the spdep and vegan developers for their foundational functions that binneR is built upon!

Send inquiries to:

Corey Devin Anderson
coreydevinanderson@gmail.com
 
