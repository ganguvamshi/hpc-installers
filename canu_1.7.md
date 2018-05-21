## Install `canu` v1.7


### Dependencies

* needs perl5 module for execution

### Downlaod and install

```
mkdir -p /app1/bioinfo/canu
cd /app1/bioinfo/canu/
git clone https://github.com/marbl/canu.git 1.7
cd 1.7/src
make -j 10

```

### Modulefile

below module file is used for canu v1.7

```
#%Module -*****-
##
## modulefile
##
set tool canu
set version 1.7
set prefix /app1/bioinfo/${tool}/${version}/Linux-amd64

proc ModulesHelp { } {
        global version prefix tool
        puts stderr "\tenvironment for Loading the $tool Library for GNU C Compiler"
}

module-whatis   "Loads the enviornment for $tool Library Version $version\n"


if { ![is-loaded perl5 ] } {
        module load perl5
}
if { ![is-loaded jre/1.8.0_162 ] } {
        module load jre/1.8.0_162
}

prereq perl5
prereq jre/1.8.0_162

prepend-path        PATH                            ${prefix}/bin

```
