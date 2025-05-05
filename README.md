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
* Copy the CDRFGcode directory to $FOAM_UTILITIES/preProcessing/:
* Compile the code in $FOAM_UTILITIES/preProcessing/CDRFGcode:
  
          $ cd $FOAM_UTILITIES/preProcessing/CDRFGcode
  
          $ ./Allwclean

          $ ./Allwmake

  The CDRFG is now compiled for use in OpenFOAM software and can be run with the ` cdrfgRun ` command in serial.

# Simulation Test

In the test folder, a setup for a simulation is provided. This simulation consists of two stages: the first stage is the execution of the CDRFG code to create an artificial turbolance flow at the inlet boundary, and the second stage is the main simulation with the LES model.

### Input parameters for CDRFG
The directory test/constant contains a file called mean_velocity_Properties, in which the inlet flow characteristics can be configured. In this file, based on the atmospheric boundary layer profile, the dependence of velocity components, turbulence intensity, and turbulence length scale on the height above ground level is specified at several points. The corresponding profile is then constructed through interpolation and extrapolation.

In the test/constant directory, the file CDRFG_Properties is also available. This file contains the settings related to the CDRFG method, including the specification of parameters, some examples of which are provided below.
* nf 100;// Number of random frequencies in one segment 
* nm   100;     // Number of frequency segments 
* nt   20;       // Number of time steps 
* fmax   100;   // Maximum frequency
* dtt   0.001;      // Time step (s)
* DGamma 0.22;      // Characteristic length used to maintain the coherency 
* Coherency  (10   10   10); //  Coherency decay constants in x, y
  
Please note that the time step and the number of solution steps specified in this file must be consistent with those defined in the controlDict file.

### Excuting the test case
In the test directory, follow the steps below.
* Generate the mesh using the following command.
  
           $ blockMesh

* Run the CDRFG code.
  
           $ cdrfgRun
  
 After running this code, the constant/boundaryData/inlet directory is generated, in which a U file is created for each time step for all inlet boundary points. Each file contains random instantaneous velocity values.

* Decompose the case:

           $ decomposePar

*  Finally run the LES case:

          $ mpirun -np 4 pisoFoam -parallel


# Reference
[1]	H. Aboshosha, A. Elshaer, G. T. Bitsuamlak, and A. El Damatty, “Consistent inflow turbulence generator for LES evaluation of wind-induced responses for tall buildings,” J. Wind Eng. Ind. Aerodyn., vol. 142, pp. 198–216, Jul. 2015







  


