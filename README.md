# SemivisibleJets

This repo contains files necessary for generation of semi-visible jet Monte Carlo signal events in `MadGraph`. 
UFO files associated with two UV completions are provided:

- `DMsimp_s_spin1`: An s-channel production mediated through a new heavy Z'. The model provided is a modified version of the spin-1 `DMsimp` model (http://feynrules.irmp.ucl.ac.be/wiki/DMsimp) 
implemented through `FeynRules`.

- `DMsimp_tchannel`: A t-channel production where the dark and visible sectors interact through a new scalar bi-fundamental.

## t-channel
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

## s-channel

```
import DMsimp_s_spin1
define j = g u c t d b s g u~ c~ t~ d~ b~ s~
generate p p > xd xd~
add process p p > xd xd~ j
add process p p > xd xd~ j j
output sig_schannel
```
