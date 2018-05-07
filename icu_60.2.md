## ICU for boost library

### Load Dependencies 
`module load gcc-7.3.0`

### Build and Install
```
./configure --prefix=/app1/centos6.3/gnu/icu/60.2
make
make install

```

### Module file 


```
#%Module -*****-
##
## modulefile
##
set tool icu
set version 60.2
set prefix /app1/centos6.3/gnu/${tool}/${version}

proc ModulesHelp { } {
        global version prefix tool
        puts stderr "\tenvironment for Loading the $tool Library for GNU C Compiler"
}

module-whatis   "Loads the enviornment for $tool Library Version $version\n"


if { ![is-loaded gcc-7.3.0 ] } {
        module load gcc-7.3.0
}

prereq gcc-7.3.0

prepend-path        PATH                            ${prefix}/bin
prepend-path        PATH                            ${prefix}/sbin
prepend-path        LD_LIBRARY_PATH                 ${prefix}/lib
prepend-path        CPATH                           ${prefix}/include
prepend-path        PKG_CONFIG_PATH                 ${prefix}/lib/pkgconfig
prepend-path        MANPATH                         ${prefix}/share/man

```  