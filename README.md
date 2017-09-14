# Power spectrums and autocorrelation functions

Contains power spectrums (.psd) and autocorrelation functions (.acf) that are used by the GPSDM code.

File format is:
  * ClockBlock-SVN-REF-label.ext

where:
  * Clock is either Rb/Cs
  * Block is either II, IIA, IIR (Rb only), or IIF
  * SVN is the two-digit SVN [15-73], or "av", which is the average over all SVNs
  * REF is the reference clock (e.g., 'USN3', 'AMC2', or also 'RbIIR'). Can be "Hmas", which means averaged over all ground-station (H-maser) references.
  * .ext is .psd for power spectrums, or .acf for autocorrelation
  * label in this case in "1280-1959"

These files are generated using the "processNoise" program.
All functions are average over data from weeks 1280-1959 [18 July 2004 -- 29 July 2017].
Days that had 10 or more missing data points were excluded from this analysis.

## PSD: power spectrums

Header lines begin with '#'.

The psd files are only used to generate fake "simulated" clock data, by the GpsSimulator in the "testLikelihoods" program.
These files are optional, the program can be used without these files (though then it will use white noise).


### File format

Note: these files only include the first half of the power spectrum (since it is symmetric).
There are three collumns, the first is generated using un-differenced data (that has had a 2-order polynomial removed), the second with first-order differenced data, and the third with second-order differenced data.

The first data point after the header file is the DC component. Each subsequent row gives the next heighest frequency component.

**Note:** Be careful when re-constructing the power spectrum, since the file only gives the first half (up to Niquiest frequency). In particular, depending on whether there are an even or odd number of points in the power spectrum will determine wether or not this highest frequency (Niquist frequency) should appear twice.
This is important, since the first-order differenced data has one fewer data points than the un-differenced data, and the second-order differenced data has two fewer.

For this reason, the first- and second-order differenced power spectrums are different lengths, but they have trailing zeros at the end of the data file.
These zeros are _not_ part of the power spectrum and should be dropped!

There are 2880, 2879, and 2878 points in the time-series (and thus the full power spectrums) for the 0, 1, 2-order differenced data.
There are therefore 1440, 1439, and 1439 points in the first half of the power spectrums for the 0, 1, 2-order differenced data, including the DC term, [Nno, the second 1439 is not a typo, it is the same due to the odd/even consideration mentioned above.]

  * All of this is taken into account in my GPSDM codes, so you don't need to worry about it.


## ACF: autocorrelation functions

Header lines begin with '#'.
The acf files are used for the 'covariance' matrix for the Bayesian likelihoods.

### File format

The first non-header row contains two data points.
These are standard deviations of the first- and second-order differenced data.
Then, each subsequent non-header collumn contains three values. Again, these are the ACF for the 0th, 1st and 2nd order differenced data.
The first ACF row should all be 1s, these are the ACF at 0 lag.
The next row is at a lag of 1 epoch (30s), then 2 epochs and so on.
The ACF is given for 128 points.



## See also:
  * Noise Profiles memo!



