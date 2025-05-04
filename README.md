# CDRFG-synthetic-turbulence-inflow
Consistent Discrete Random Flow Generation method (CDRFG)was introduced by Aboshosha et al [1]. This approach retains the ability to produce turbulence fields with any desired power spectrum while maintaining coherence between velocity components.
Using this method and with the available data on mean velocity distribution and turbulence intensity at the inlet plane, it is possible to generate a random turbulent flow field at all inlet points with a desired time step.
The code is developed as a utility application using OpenFOAM as a framwork.

# Installing CDRFG
### Requirements
* OpenFOAM, preferably v8

The code provided was written for OpenFoam version 8 and requires modifications for use in higher versions of the software.
### Build from source
Follow the instructions below:

* Clone the code to your computer:
* Copy the CDRFGcede directory to $FOAM_UTILITIES/preProcessing/:
* Compile the code in $FOAM_UTILITIES/preProcessing/CDRFGcede:
  
          $ cd $FOAM_UTILITIES/preProcessing/CDRFGcede
  
          $ ./Allwclean

          $ ./Allwmake


