# Helmfile

For the baseline infrastructure services that I want running on my Pi cluster I
use [helmfile](https://github.com/helmfile/helmfile) to setup everything with
one command[^1].

[^1] Almost: after applying the helmfile in a fresh install of my cluster I need
to manually configure my nodes in Longhorn to use the correct (USB) drives.
