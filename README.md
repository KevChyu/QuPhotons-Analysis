Improved Photon Data Simulation

This repository contains a Jupyter Notebook (Improved_Photon_Data.ipynb) designed to simulate and analyze photon detection events using Single Photon Avalanche Diodes (SPADs). 
It provides a comprehensive workflow for signal generation and cross-correlation delay analysis, originally developed within a quantum optics signal generation directory.  
OverviewThe simulation models photon arrivals over millions of subsequences, applying defined probability distributions to mimic real-world optical pulses. 
It processes the temporal data to identify coincidences and time gaps between two separate detector channels (SPAD0 and SPAD1), ultimately extracting the modified cross-correlation delay.  

Features
Pulse Shape Libraries: 
Includes multiple probability distribution functions for temporal pulse modeling, such as:
Super-Gaussian (Rounded Rectangle)  
Gamma distribution  
Tanh (Sigmoid-edged flat top)  
Trapezoid (Linear ramp up/down)  
Tukey window (Cosine-tapered flat top)  
Super-Lorentzian  
Error-function (erf) flat top  
Vectorized Event Generation: Efficiently simulates large datasets—such as generating roughly 14.89 million photon events across 5,000,000 subsequences—using memory-bounded chunk processing and NumPy vectorization.  
Temporal Masking: Filters the generated dataset down to a specific Region of Interest (ROI) (e.g., 1100 ns to 1900 ns).  
Neighboring Event Correlation: Sorts and calculates the exact time gaps between temporally adjacent photons occurring on different SPADs.  
Background Envelope Subtraction: Isolates sequences containing exactly one photon per SPAD, applies a linear fit to the symmetric tails to calculate the accidental coincidence envelope, and subtracts it to reveal the normalized cross-correlation delay.  

Dependencies
The notebook requires a standard scientific Python environment. The following libraries must be installed and imported:
numpy  
matplotlib.pyplot  
scipy.stats (specifically poisson and gamma)  
scipy.special (erf) 
Standard Python libraries: os, glob, math  

Project Workflow
Parameter Initialization: Sets global experimental parameters, such as defining the pulse start time at 1000 ns, end time at 2000 ns, and sampling gaps at 5 ns.  
Probability Array Generation: Constructs the baseline probability per tick using the selected pulse envelope function.  
Simulation Loop: Iterates through subsequences in discrete chunks to generate stochastic photon arrivals, recording the sequence index, tick index, and SPAD index for each event.  
Data Visualization: Generates side-by-side histograms displaying the raw total arrivals and the specific ROI overlays for SPAD0 and SPAD1.  
Time Gap Extraction: Computes the delay between detector hits for valid neighboring pairs.  
Envelope Fitting: Analyzes single-photon-pair sequences and applies a linear polyfit to the absolute time gaps within a specified fit region (e.g., 150 ns to 550 ns) to determine the background slope and intersection.  
Final Output: Plots the raw and normalized modified data, illustrating the cross-correlation delay after background envelope subtraction.  
