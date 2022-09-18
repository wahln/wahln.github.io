---
layout: page
title: matRad
description: An open source dose calculation and treatment planning toolkit for radiotherapy research and education
img: assets/img/matrad_hat.svg
importance: 1
category: pi
---

# matRad: An open source dose calculation and treatment planning toolkit for research and education

[matRad](http://matrad.org) is an open source software for radiation treatment planning of intensity-modulated photon, proton, and carbon ion therapy started in 2015 in the research group [Radiotherapy Optimization](https://www.dkfz.de/radopt) within the [Division of Medical Physics in Radiation Oncology](https://www.dkfz.de/en/medphys/) at the [German Cancer Research Center - DKFZ](https://www.dkfz.de). 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="/assets/img/matRad_UI.png" title="matRad GUI" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    matRad's graphical user interface
</div>


[matRad](http://matrad.org) targets education and research in radiotherapy treatment planning, where the software landscape is dominated by proprietary medical software. As of August 2022, [matRad](http://matrad.org) had more than 130 forks on GitHub and its [development paper](https://doi.org/10.1002/mp.12251) was cited more than 160 times (according to Google Scholar). matRad is entirely written in MATLAB and mostly compatible to GNU Octave.

[matRad](http://matrad.org) comprises
- MATLAB functions to model the entire treatment planning workflow
- Example patient data from the CORT dataset
- Physical and biological base data for all required computations

In particular we provide functionalities for

- Pencil-beam dose calculation for photon IMRT and proton/carbon IMPT
- Monte Carlo dose calculation for photon IMRT (with ompMC) and proton IMPT (with [MCsquare](http://www.openmcsquare.org))
- Non-linear constrained treatment plan optimization (based on physical dose, RBE-weighted dose and biological effect) using [IPOPT](https://coin-or.github.io/Ipopt/) or Matlab's fmincon
- Multileaf collimator sequencing
- Basic treatment plan visualization and evaluation
- Graphical User Interface
- Standalone Executable (using the Matlab Runtime)

[matRad](http://matrad.org) is constantly evolving. If you are interested in working with us or are looking for a special feature do not hesitate and get in touch.

## Philosophy

<div class="row">
    <div class="col-sm-8">
        matRad provides a graphical user interface for educational purposes and basic treatment plan prameterization and visualization, but mainly uses Matlab's dual scripting & visualization environment to allow a parallel workflow, alternating between scripting / command line input and triggering workflow steps in the graphical user interface.
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="/assets/img/matrad_philosophy.png" title="matRad GUI" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

A script to recreate the above treatment plan within [matRad](http://matrad.org) 2.10.1 is shown below:

```matlab
matRad_rc

% load patient data, i.e. ct, voi, cst
load PROSTATE.mat

% meta information for treatment plan
pln.radiationMode   = 'carbon';     % either photons / protons / carbon
pln.machine         = 'Generic';

pln.numOfFractions  = 30;

% beam geometry settings
pln.propStf.bixelWidth      = 5; % [mm] / lateral spot spacing for particles
pln.propStf.gantryAngles    = [90 270]; % [?]
pln.propStf.couchAngles     = [0 0]; % [?]
pln.propStf.numOfBeams      = numel(pln.propStf.gantryAngles);
pln.propStf.isoCenter       = ones(pln.propStf.numOfBeams,1) * matRad_getIsoCenter(cst,ct,0);

% dose calculation settings
pln.propDoseCalc.doseGrid.resolution.x = 5; % [mm]
pln.propDoseCalc.doseGrid.resolution.y = 5; % [mm]
pln.propDoseCalc.doseGrid.resolution.z = 5; % [mm]

% optimization settings
pln.propOpt.optimizer       = 'IPOPT';
pln.propOpt.bioOptimization = 'LEMIV_effect';   

%% generate steering file
stf = matRad_generateStf(ct,cst,pln);

%% dose calculation
dij = matRad_calcParticleDose(ct,stf,pln,cst);

%% inverse planning for imrt
resultGUI = matRad_fluenceOptimization(dij,cst,pln);

%% start gui for visualization of result
matRadGUI
```

For educational purposes, matRad is also available as a standalone application.

