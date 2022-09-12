# Semi-visible Jets

[![arXiv](https://img.shields.io/badge/arXiv-1707.05326%20-green.svg)](https://arxiv.org/abs/1707.05326)

> ⚠️ **Discalimer**: The contents of this repository are outdated and no longer maintained. While they may provide a useful starting point, the files here should not be used in production as is. See notes below for known issues. [This fork](https://github.com/eshwen/SemivisibleJets/) may contain more up-to-date files and instructions for event generation.

This repository contains model files necessary for generation of semi-visible jet Monte Carlo signal events in `MadGraph`. 
Please see [1707.05326](https://arxiv.org/abs/1707.05326) and [1503.00009](https://arxiv.org/abs/1503.00009) for
for further details. Please note that a recent version of `PYTHIA` (> 8.226) including the Hidden Valley module 
and running of the dark coupling is required when implementing the subsequent dark hadronization.

UFO files associated with two UV completions are provided:

## s-channel production

An s-channel production (`DMsimp_s_spin1`) mediated through a new heavy Z'. The model provided is a modified version of the spin-1 `DMsimp` model (http://feynrules.irmp.ucl.ac.be/wiki/DMsimp) 
implemented through `FeynRules`.

## t-channel production

A t-channel production (`DMsimp_tchannel`) where the dark and visible sectors interact through a new scalar bi-fundamental.

The bi-fundamentals are denoted with `su11, su12, su21, su22...`, where `u` etc explicitly specifies the QCD flavour index 
and the numbers are the explicit dark non-Abelian group indices. Similarly, the dark quarks are labeled as `qv11, qv12, qv21, qv22`.

A `FeynRules` model file (`DMsimp_tchannel.fr`) as well as the `Mathematica` notebook (`DMsimp_tchannel.nb`) used to generated the UFO output 
are also provided.

### Notes on event generation with the t-channel mediator

Please note that a modified version of `MadGraph` using the patch included [here](https://bugs.launchpad.net/mg5amcnlo/+bug/1702712) 
is required to ensure a stable cross section for event generation using this model.

Additionally, the `param_card.dat` generated while running t-channel production may assumed a fixed width for the mediator, which may not be desired. In this case, the `param_card.dat` can be manually modified as follows to automatically compute the mediator width (see [here](https://answers.launchpad.net/mg5amcnlo/+question/215238) for discussion):
```
DECAY 9000005 Auto
DECAY 9000006 Auto
...
DECAY 9000028 Auto
```

## Example `MadGraph` production

- Inclusive s-channel production:
```
import DMsimp_s_spin1
define j = g u c t d b s g u~ c~ t~ d~ b~ s~
generate p p > xd xd~
add process p p > xd xd~ j
add process p p > xd xd~ j j
output sig_schannel
```
- Inclusive t-channel production:
```
import DMsimp_tchannel
define gv = gv11 gv12 gv21 gv22
define gv~ = gv11~ gv12~ gv21~ gv22~
define j = g u c t d b s g u~ c~ t~ d~ b~ s~
generate p p > gv gv~
add process p p > gv gv~ j
add process p p > gv gv~ j j
output sig_tchannel
```

## Note on hadronization with `PYTHIA`

As noted above, a recent version of `PYTHIA` (>~ 8.226) including the Hidden Valley (HV) module 
and running of the dark coupling is required when implementing the subsequent dark hadronization.

In order to be able to use the HV module, the PDG IDs of the dark particles must be changed in the LHE files
for `PYTHIA` to be 
able to recognize and shower these properly. This can be done as follows:

- For the s-channel model
```
sed -i 's/5000521/4900101/g' <LHE filename>
```
- For the t-channel model
```
sed -i 's/49001010/4900101/g' <LHE filename>	
sed -i 's/49001011/4900101/g' <LHE filename>	
sed -i 's/49001012/4900101/g' <LHE filename>	
sed -i 's/49001013/4900101/g' <LHE filename>	
sed -i 's/49001014/4900101/g' <LHE filename>	
```

## Contact

For questions or issues please contact:

-  Tim Lou; hlou at berkeley dot edu
-  Siddharth Mishra-Sharma; smsharma at princeton dot edu
