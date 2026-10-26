# Preprocessing, Denoising, Quality Control steps

Methods

Analyses of fMRI data were performed using CONN[1] (RRID:SCR_009550) release 25.b[2] and SPM[3] (RRID:SCR_007037) release 25.01.02.

Preprocessing: Functional and anatomical data were preprocessed using a modular preprocessing pipeline[4] including realignment with correction of susceptibility distortion interactions, slice timing correction, outlier detection, direct coregistration to structural, direct segmentation and MNI-space normalization, and smoothing. Functional data were realigned using SPM realign & unwarp procedure[5], where all scans were coregistered to a reference image (first scan of the first session) using a least squares approach and a 6 parameter (rigid body) transformation[6], and resampled using b-spline interpolation to correct for motion and magnetic susceptibility interactions. Temporal misalignment between different slices of the functional data (acquired in ascending order) was corrected following SPM slice-timing correction (STC) procedure[7,8], using sinc temporal interpolation to resample each slice BOLD timeseries to a common mid-acquisition time. Potential outlier scans were identified using ART[9] as acquisitions with framewise displacement above 0.5 mm or global BOLD signal changes above 3 standard deviations[10,11], and a reference BOLD image was computed for each subject by averaging all scans excluding outliers. Functional and anatomical data were coregistered using SPM intermodality coregistration procedure[12] with a normalised mutual information objective function[13]. Functional and anatomical data were normalized into standard MNI space, segmented into grey matter, white matter, and CSF tissue classes, and resampled to 2 mm isotropic voxels following a direct normalization procedure[11,14] using SPM unified segmentation and normalization algorithm[15,16] with the default IXI-549 tissue probability map template. Last, functional data were smoothed using spatial convolution with a Gaussian kernel of 8 mm full width half maximum (FWHM).

Denoising: In addition, functional data were denoised using a confound regression pipeline incorporating established nuisance regressors[17]. This included the removal of potential confounding effects derived from white matter (10 regressors), CSF (5 regressors), motion parameters and their first order derivatives (12 regressors)[18], outlier scans (<36 regressors)[10], session and task effects and their first order derivatives (8 regressors), and linear trends (2 regressors) within each functional run, followed by bandpass frequency filtering of the BOLD timeseries[19] between 0.008 Hz and 0.09 Hz. CompCor regressors[20,21] were estimated within each subject's eroded white matter and CSF masks by extracting the mean signal and the largest principal components orthogonal to the mean signal, motion parameters, and outlier scans. Based on the number of nuisance regressors included, the effective temporal degrees of freedom of the denoised BOLD signal ranged from 132.5 to 155.5 (mean 147.5) across subjects[11].

Quality Control (QC): Quality Control procedures included the computation of Data Validity, Quality, and Sensitivity scores, providing quantitative assessments of global distributional biases, motion-related confounds, and group-level sensitivity to small FC effects after preprocessing and denoising. First, global biases in FC estimates were characterized by the Data Validity score, measuring the displacement of the empirical FC distribution peak from zero, its expected value in the absence of systematic biases[22]. Second, motion and outlier-related confounds were evaluated using QC-FC correlations[23] between FC values and subject motion and outlier-prevalence measures. These effects were summarized by the Data Quality score, defined as the Overlap Coefficient between the observed QC-FC correlation distribution and its permutation-derived null distribution[24,11]. Last, Sensitivity was quantified as the statistical power to detect a small target FC effect (r=0.1) in a fixed-effects analysis, using a Welch-Satterthwaite approximation for effective degrees of freedom[25], and excluding participants whose QC metrics were extreme outliers (values more than three interquartile ranges beyond the first or third quartile). Data Validity, Quality, and Sensitivity scores are expressed in percent units and interpreted using three broad categories: low (<80%), intermediate (80–95%), and high (>95%) values. After preprocessing and denoising, the dataset yielded high Data Validity (100%), high Data Quality (99%), and high Sensitivity scores (100%). Detailed QC statistics and plots are provided in the Appendix.

References
[1] Whitfield-Gabrieli, S., & Nieto-Castanon, A. (2012). Conn: a functional connectivity toolbox for correlated and anticorrelated brain networks. Brain connectivity, 2(3), 125-141.

[2] Nieto-Castanon, A. & Whitfield-Gabrieli, S. (2025). CONN functional connectivity toolbox, Version 25: RRID SCR_009550. doi:10.56441/hilbertpress.2538.3958

[3] Penny, W. D., Friston, K. J., Ashburner, J. T., Kiebel, S. J., & Nichols, T. E. (Eds.). (2011). Statistical parametric mapping: the analysis of functional brain images. Elsevier.

[4] Nieto-Castanon, A. (2020). FMRI minimal preprocessing pipeline. In Handbook of functional connectivity Magnetic Resonance Imaging methods in CONN (pp. 3–16). Hilbert Press.

[5] Andersson, J. L., Hutton, C., Ashburner, J., Turner, R., & Friston, K. J. (2001). Modeling geometric deformations in EPI time series. Neuroimage, 13(5), 903-919.

[6] Friston, K. J., Ashburner, J., Frith, C. D., Poline, J. B., Heather, J. D., & Frackowiak, R. S. (1995). Spatial registration and normalization of images. Human brain mapping, 3(3), 165-189.

[7] Henson, R. N. A., Buechel, C., Josephs, O., & Friston, K. J. (1999). The slice-timing problem in event-related fMRI. NeuroImage, 9, 125.

[8] Sladky, R., Friston, K. J., Tröstl, J., Cunnington, R., Moser, E., & Windischberger, C. (2011). Slice-timing effects and their correction in functional MRI. Neuroimage, 58(2), 588-594.

[9] Whitfield-Gabrieli, S., Nieto-Castanon, A., & Ghosh, S. (2011). Artifact detection tools (ART). Cambridge, MA. Release Version, 7(19), 11.

[10] Power, J. D., Mitra, A., Laumann, T. O., Snyder, A. Z., Schlaggar, B. L., & Petersen, S. E. (2014). Methods to detect, characterize, and remove motion artifact in resting state fMRI. Neuroimage, 84, 320-341.

[11] Nieto-Castanon, A. (2025). Preparing fMRI data for statistical analysis. In fMRI techniques and protocols (pp. 163-191). New York, NY: Springer US.

[12] Ashburner, J., & Friston, K. (1997). Multimodal image coregistration and partitioning—a unified framework. Neuroimage, 6(3), 209-217.

[13] Studholme, C., Hawkes, D. J., & Hill, D. L. (1998, June). Normalized entropy measure for multimodality image alignment. In Medical imaging 1998: image processing (Vol. 3338, pp. 132-143). SPIE.

[14] Calhoun, V.D., Wager, T.D., Krishnan, A., Rosch, K.S., Seymour, K.E., Nebel, M.B., Mostofsky, S.H., Nyalakanai, P. and Kiehl, K. (2017). The impact of T1 versus EPI spatial normalization templates for fMRI data analyses (Vol. 38, No. 11, pp. 5331-5342).

[15] Ashburner, J., & Friston, K. J. (2005). Unified segmentation. Neuroimage, 26(3), 839-851.

[16] Ashburner, J. (2007). A fast diffeomorphic image registration algorithm. Neuroimage, 38(1), 95-113.

[17] Nieto-Castanon, A. (2020). FMRI denoising pipeline. In Handbook of functional connectivity Magnetic Resonance Imaging methods in CONN (pp. 17–25). Hilbert Press.

[18] Friston, K. J., Williams, S., Howard, R., Frackowiak, R. S., & Turner, R. (1996). Movement-related effects in fMRI time-series. Magnetic resonance in medicine, 35(3), 346-355.

[19] Hallquist, M. N., Hwang, K., & Luna, B. (2013). The nuisance of nuisance regression: spectral misspecification in a common approach to resting-state fMRI preprocessing reintroduces noise and obscures functional connectivity. Neuroimage, 82, 208-225.

[20] Behzadi, Y., Restom, K., Liau, J., & Liu, T. T. (2007). A component based noise correction method (CompCor) for BOLD and perfusion based fMRI. Neuroimage, 37(1), 90-101.

[21] Chai, X. J., Nieto-Castanon, A., Ongur, D., & Whitfield-Gabrieli, S. (2012). Anticorrelations in resting state networks without global signal regression. Neuroimage, 59(2), 1420-1428.

[22] Morfini F, Whitfield-Gabrieli S and Nieto-Castañón A (2023) Functional connectivity MRI quality control procedures in CONN. Front. Neurosci. 17:1092125.

[23] Ciric, R., Wolf, D. H., Power, J. D., Roalf, D. R., Baum, G. L., Ruparel, K., et al. (2017). Benchmarking of participant-level confound regression strategies for the control of motion artifact in studies of functional connectivity. NeuroImage 154, 174–187.

[24] Inman, H. F., & Bradley Jr, E. L. (1989). The overlapping coefficient as a measure of agreement between probability distributions and point estimation of the overlap of two normal densities. Communications in Statistics-theory and Methods, 18(10), 3851-3874.

[25] Satterthwaite, F. E. (1946). An approximate distribution of estimates of variance components. Biometrics bulletin, 2(6), 110-114.

# 1st-level Analysis

## SBC

First-level analysis SBC_01: Seed-based connectivity maps (SBC) and ROI-to-ROI connectivity matrices (RRC) were estimated characterizing the patterns of functional connectivity with 432 ROIs. Functional connectivity strength was represented by Fisher-transformed bivariate correlation coefficients from a weighted general linear model (weighted-GLM[4]), defined separately for each pair of seed and target areas, modeling the association between their BOLD signal timeseries.

References
[1] Whitfield-Gabrieli, S., & Nieto-Castanon, A. (2012). Conn: a functional connectivity toolbox for correlated and anticorrelated brain networks. Brain connectivity, 2(3), 125-141.

[2] Nieto-Castanon, A. & Whitfield-Gabrieli, S. (2025). CONN functional connectivity toolbox, Version 25: RRID SCR_009550. doi:10.56441/hilbertpress.2538.3958

[3] Penny, W. D., Friston, K. J., Ashburner, J. T., Kiebel, S. J., & Nichols, T. E. (Eds.). (2011). Statistical parametric mapping: the analysis of functional brain images. Elsevier.

[4] Nieto-Castanon, A. (2020). Functional Connectivity measures. In Handbook of functional connectivity Magnetic Resonance Imaging methods in CONN (pp. 26–62). Hilbert Press.

##RRC
First-level analysis RRC_01: ROI-to-ROI connectivity (RRC) matrices were estimated characterizing the functional connectivity between each pair of regions among 564 ROIs. Functional connectivity strength was represented by Fisher-transformed bivariate correlation coefficients from a general linear model (weighted-GLM[4]), estimated separately for each pair of ROIs, characterizing the association between their BOLD signal timeseries. Individual scans were weighted by a boxcar signal characterizing each individual task or experimental condition convolved with an SPM canonical hemodynamic response function and rectified.

References
[1] Whitfield-Gabrieli, S., & Nieto-Castanon, A. (2012). Conn: a functional connectivity toolbox for correlated and anticorrelated brain networks. Brain connectivity, 2(3), 125-141.

[2] Nieto-Castanon, A. & Whitfield-Gabrieli, S. (2025). CONN functional connectivity toolbox, Version 25: RRID SCR_009550. doi:10.56441/hilbertpress.2538.3958

[3] Penny, W. D., Friston, K. J., Ashburner, J. T., Kiebel, S. J., & Nichols, T. E. (Eds.). (2011). Statistical parametric mapping: the analysis of functional brain images. Elsevier.

[4] Nieto-Castanon, A. (2020). Functional Connectivity measures. In Handbook of functional connectivity Magnetic Resonance Imaging methods in CONN (pp. 26–62). Hilbert Press.

# 2nd-level Analysis

Group-level analyses were performed using a General Linear Model (GLM[4]). For each individual voxel a separate GLM was estimated, with first-level connectivity measures at this voxel as dependent variables (one independent sample per subject and one measurement per task or experimental condition, if applicable), and groups or other subject-level identifiers as independent variables. Voxel-level hypotheses were evaluated using multivariate parametric statistics with random-effects across subjects and sample covariance estimation across multiple measurements. Inferences were performed at the level of individual clusters (groups of contiguous voxels). Cluster-level inferences were based on parametric statistics from Gaussian Random Field theory[5,6]. Results were thresholded using a combination of a cluster-forming p < 0.001 voxel-level threshold, and a familywise corrected p-FDR < 0.05 cluster-size threshold[7].

References
[1] Whitfield-Gabrieli, S., & Nieto-Castanon, A. (2012). Conn: a functional connectivity toolbox for correlated and anticorrelated brain networks. Brain connectivity, 2(3), 125-141.

[2] Nieto-Castanon, A. & Whitfield-Gabrieli, S. (2025). CONN functional connectivity toolbox, Version 25: RRID SCR_009550. doi:10.56441/hilbertpress.2538.3958

[3] Penny, W. D., Friston, K. J., Ashburner, J. T., Kiebel, S. J., & Nichols, T. E. (Eds.). (2011). Statistical parametric mapping: the analysis of functional brain images. Elsevier.

[4] Nieto-Castanon, A. (2020). General Linear Model. In Handbook of functional connectivity Magnetic Resonance Imaging methods in CONN (pp. 63–82). Hilbert Press.

[5] Worsley, K. J., Marrett, S., Neelin, P., Vandal, A. C., Friston, K. J., & Evans, A. C. (1996). A unified statistical approach for determining significant signals in images of cerebral activation. Human brain mapping, 4(1), 58-73.

[6] Nieto-Castanon, A. (2020). Cluster-level inferences. In Handbook of functional connectivity Magnetic Resonance Imaging methods in CONN (pp. 83–104). Hilbert Press.

[7] Chumbley, J., Worsley, K., Flandin, G., & Friston, K. (2010). Topological FDR for neuroimaging. Neuroimage, 49(4), 3057-3064.
