## Install `proovread` v2.14.0


### Dependencies

* needs perl5 module for execution
* ncbi blast+ 
* samtools/1.6

### Downlaod and install

```
cd /app1/bioinfo/sources
git clone https://github.com/BioInf-Wuerzburg/proovread
cd proovread
module load perl5 blast+ samtools/1.6
make 
make install PREFIX=/app1/bioinfo/proovread/2.14.0

```

### Testing 

```
cd /app1/bioinfo/proovread/2.14.0
add `use forks` to bin/proovread file
make sample
# load the needed modules if not preloaded
```
### Modulefile

below module file is used for proovread v2.14.0

```
#%Module -*****-
##
## modulefile
##
set tool proovread
set version 2.14.0
set prefix /app1/bioinfo/${tool}/${version}

proc ModulesHelp { } {
        global version prefix tool
        puts stderr "\tenvironment for Loading the $tool Library for GNU C Compiler"
}

module-whatis   "Loads the enviornment for $tool Library Version $version\n"


if { ![is-loaded perl5 ] } {
        module load perl5
}

if { ![is-loaded blast+ ] } {
        module load blast+
}

if { ![is-loaded samtools/1.6 ] } {
        module load samtools/1.6
}

prereq perl5
prereq blast+
prereq samtools/1.6

prepend-path        PATH                            ${prefix}/bin

```
