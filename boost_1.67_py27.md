## Installing boost 1.67 with python2.7 support


### Load dependencies

`module load gcc-7.3.0 python2.7 icu/60.2`

### Build, Compile and Install

```
BOOST_DIR=/app1/centos6.3/sources/boost_1_67_0
cd $BOOST_DIR
./bootstrap.sh --with-libraries=python,serialization --with-python=python2.7  --with-python-root=/app1/centos6.3/gnu/python-2.7.8 --prefix=/app1/centos6.3/gnu/boost/1.67_py27/ --with-icu=/app1/centos6.3/gnu/icu/60.2


./b2 
./b2 install

```

### Module file for `boost_py3`
```
#%Module1.0

set     version         1.67_py27
set     prefix          /app1/centos6.3/gnu
set     tool            boost

proc ModulesHelp { } {
        global version prefix tool

        puts stderr "\t Adss $tool v$version to environment\n"
}

if { ![is-loaded gcc-7.3.0 ] } {
        module load gcc-7.3.0
}

if { ![is-loaded python2.7 ] } {
        module load python2.7
}

prereq python2.7
prereq gcc-7.3.0

module-whatis   "Loads $tool v$version"

set                     root                    ${prefix}/${tool}/${version}
set                     BOOSTROOT               ${root}
#setenv                 BOOSTROOT               ${root}
setenv                  BOOST_ROOT              ${root}
setenv                  BOOST_LIBRARYDIR        ${root}/lib
prepend-path            LD_LIBRARY_PATH         ${BOOSTROOT}/lib
prepend-path            CPATH                   ${BOOSTROOT}/include
setenv                  BOOST_INCLUDEDIR        ${BOOSTROOT}/include

```

