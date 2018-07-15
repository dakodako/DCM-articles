
# A DCM for resting state fMRI
This note will try to understand DCM using the code 
```matlab
function DEM_demo_induced_fMRI
```
provided by SPM12

## Cross spectra and cross covariance
### Cross spectra
```matlab
function [mar,y,y_pred] = spm_mar (X,p,prior,verbose)
function [mar] = spm_mar_spectra (mar,freqs,ns,show)
```
These two functions are based on paper "Variational Bayes for Generalized Autoregressive Models"

Cross spectral density is the Fourier transform of cross variance function
```matlab
function [ccf,pst] = spm_csd2ccf(csd,Hz,dt)
```
converts cross spectral density to cross covariance function
## Priors
Bayesian estimations are used in two different parts for DCM.
Variational Bayes is used to estimate the cross spectral density of the outputs.
The hidden states for DCM are estimated by EM algorithm in the model inversion part.

Priors functions need to be defined when estimating parameters in the model using Bayesian method. These prior functions is found by the following function.
```matlab
function [pE,pC,x] = spm_dcm_fmri_priors(A,B,C,D,options)
% A,B,C,D - constraints on connections
% pE - prior expectations
% pC - prior covariances
% x - prior (initial) states
A = DCM.a % switch on endogenous connections
B = DCM.b % switch on bilinear modulations
C = DCM.c % switch on exgenous connections
D = DCM.d % switch on nonlinear modulations

```
## Model inversion
Bayesian inversion of nonlinear models - Gauss-Newton/Variational Laplace
```matlab
function [Ep,Cp,Eh,F,L,dFdp,dFdpp] = spm_nlsi_GN(M,U,Y)
% M contains the information about the model such as the prior functions 
% U contains the input to the model, for resting state fMRI, the input is usually 0
% Y contains the model output, for resting state fMRI, this will be the second order data feature, cross spectra instead of the time series data
```
## Problem: Developing an accurate spectral estimation method for short-period signal
### Possible solutions:
* "Optimal spectral tracking — Adapting to dynamic regime change"
John-Stuart Brittaina, David M. Halliday

* This article is basd on "Optimal Spectral Tracking - With application to speed dependent nueral modulation of tibialis anterior during human treadmill walking"

?? Epoch based frequency analysis?

Divide the time series in to N segments

Calculate the periodogram for each segment?


# Variational Bayes for Generalized Autoregressive Models

## Negative variational free energy

# Dynamic effective connectivity in resting state fMRI

## Hidden Markov Model 

using Hidden Markov Model to model the hidden neural states, where each state corresponds to a particular point in the parameter space of effective connectivity. This effective connectivity then generates complex cross spectral data features of the observed timeseries. 

