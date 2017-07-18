# SemivisibleJets

This repo contains files necessary for generation of semi-visible jet Monte Carlo signal events in `MadGraph`. 
UFO files associated with two UV completions are provided:

### `DMsimp_s_spin1`

An s-channel production mediated through a new heavy Z'. The model provided is a modified version of the spin-1 `DMsimp` model (http://feynrules.irmp.ucl.ac.be/wiki/DMsimp) 
implemented through `FeynRules`.

### `DMsimp_tchannel`

A t-channel production where the dark and visible sectors interact through a new scalar bi-fundamental.

The bi-fundamentals are denoted with `su11, su12, su21, su22...`, where `u` etc explicitly specifies the QCD flavour index 
and the numbers are the explicit dark non-Abelian group indices.

Please note that a modified version of `MadGraph` using the patch included [here](https://bugs.launchpad.net/mg5amcnlo/+bug/1702712) 
is required to ensure a stable cross section for event generation using this model.

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

