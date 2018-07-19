## Installing the nodejs 8.11.2 library

installing `nodejs` as it is prerequisite for installing jupyterhub    

### Dependencies

* gcc-7.3.0
* python2.7 

### Compile and Install

```
SRCDIR=/app1/centos6.3/sources/node-v8.11.2

cd $SRCDIR 
./configure --prefix=/app1/centos6.3/gnu/node/8.11.2
make -j4
make install

```
### module file

```
#%Module -*****-
##
## modulefile
##
set tool node
set version 8.11.2
set prefix /app1/centos6.3/gnu

proc ModulesHelp { } {
        global version prefix tool
        puts stderr "\tenvironment for Loading the $tool Library for GNU C Compiler"
}

module-whatis   "Loads the enviornment for $tool Library Version $version\n"

set     root    ${prefix}/${tool}/${version}

if { ![is-loaded gcc-7.3.0 ] } {
        module load gcc-7.3.0
}
if { ![is-loaded python2.7 ] } {
        module load python2.7
}
prereq gcc-7.3.0
prereq python2.7

prepend-path            PATH                            ${root}/bin
prepend-path            LD_LIBRARY_PATH                 ${root}/lib
prepend-path            LIBRARY_PATH                    ${root}/lib
prepend-path            MANPATH                         ${root}/share/man
prepend-path            CPATH                           ${root}/include
```