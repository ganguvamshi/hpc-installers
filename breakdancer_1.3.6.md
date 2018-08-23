# Breakdancer

installing breakdancer, cmake module is required for compiling and installation only.

## Download, Compile and Install

This is compiled on atals7 

```
cd /app1/bioinfo/source/git/
git clone --recursive https://github.com/genome/breakdancer.git
cd breakdancer
mkdir build && cd build

module load cmake/3.9.3 
cmake -DCMAKE_BUILD_TYPE=release -DCMAKE_INSTALL_PREFIX=/app1/bioinfo/breakdancer/1.3.6 ..
```

## Modulefile

```
#%Module -*****-
##
## modulefile
##
set tool breakdancer
set version 1.3.6
set prefix /app1/bioinfo/${tool}/${version}

proc ModulesHelp { } {
        global version prefix tool
        puts stderr "\tenvironment for Loading the $tool Library for GNU C Compiler"
}

module-whatis   "Loads the enviornment for $tool Library Version $version\n"


prepend-path        PATH                                        ${prefix}/bin
prepend-path        LD_LIBRARY_PATH                             ${prefix}/lib
prepend-path        LIBRARY_PATH                                ${prefix}/lib
```