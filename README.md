# SemivisibleJets

Signal generation in MadGraph:

## t-channel
```
import DMsimp_tchannel
define gv = gv11 gv12 gv21 gv22
define gv~ = gv11~ gv12~ gv21~ gv22
generate p p > gv gv~
output tchannel_direct
```

## s-channel

```
import DMsimp_s_spin1
generate p p > xd xd~
output schannel_direct
```
