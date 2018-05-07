## Installing the htslib 1.8 library

the `htslib` is a major dependency for most of the bioinformatics software, especially `samtools` and `bcftools` which are widely used in variant analysis using NGS

### Dependencies

No major dependencies are required for this

### Compile and Install

```
SRCDIR=/app1/bioinfo/source/htslib-1.8

cd $SRCDIR 
./configure --prefix=/app1/bioinfo/htslib/1.8
make
make install

```
### module file

```
#%Module -*****-
##
## modulefile
##
set tool htslib
set version 1.8
set prefix /app1/bioinfo

proc ModulesHelp { } {
        global version prefix tool
        puts stderr "\tenvironment for Loading the $tool Library for GNU C Compiler"
}

module-whatis   "Loads the enviornment for $tool Library Version $version\n"

set     root    ${prefix}/${tool}/${version}

setenv          HTSLIB_LIBRARY_DIR      ${root}/lib
setenv          HTSLIB_INCLUDE_DIR      ${root}/include

prepend-path            PATH                            ${root}/bin
prepend-path            LD_LIBRARY_PATH                 ${root}/lib
prepend-path            LIBRARY_PATH                    ${root}/lib
prepend-path            MANPATH                         ${root}/share/man
prepend-path            CPATH                           ${root}/include
```