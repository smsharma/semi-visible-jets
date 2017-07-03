# SemivisibleJets

Signal generation in MadGraph:

## t-channel
```
import DMsimp_tchannel
define gv = gv11 gv12 gv21 gv22
define gv~ = gv11~ gv12~ gv21~ gv22
define sq = sd11 sd12 sd21 sd22 ss11 ss12 ss21 ss22 sb11 sb12 sb21 sb22
define sq~ = sd11~ sd12~ sd21~ sd22~ ss11~ ss12~ ss21~ ss22~ sb11~ sb12~ sb21~ sb22
define jj = g u c t d b s
define jj~ = g u~ c~ t~  d~ b~ s~
generate p p > gv gv~
output tchannel_direct
```

## s-channel

```
import DMsimp_s_spin1
define jj = g u c t d b s
define jj~ = g u~ c~ t~  d~ b~ s~
generate p p > xd xd~
output schannel_direct
```
