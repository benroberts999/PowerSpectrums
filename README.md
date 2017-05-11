# PowerSpectrums
Contains power spectrums (.psd) and autocorrelation functions (.acf) that are used by the GPSDM code.

Both of these files are generated using the "processNoise" program.

The psd files are only used to generate fake "simulated" clock data, by the "testLikelihoods" program.
This program can be used without these files, though you must select 'white noise'.

The acf files are used for the 'covariance' matrix.
Again, the code will work without these files, however, you must choose "0" points for the Eij.
--that part of the code is still being developed.
