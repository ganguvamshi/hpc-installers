## Installing boost 1.67 with python3 support


### Load dependencies

`module load gcc-7.3.0 python3.6.4 icu/60.2`

### Build, Compile and Install

```
BOOST_DIR=/app1/centos6.3/sources/boost_1_67_0
cd $BOOST_DIR
./bootstrap.sh --with-libraries=python,serialization --with-python=python3.6  --with-python-root=/app1/centos6.3/gnu/Python-3.6.4 --prefix=/app1/centos6.3/gnu/boost/1.67_py3/ --with-icu=/app1/centos6.3/gnu/icu/60.2
# add this line to python.congured section within project-config.jam file
/app1/centos6.3/gnu/Python-3.6.4/include/python3.6m

./b2 
./b2 install

```

### Module file for `boost_py3`

#%Module1.0

```
set     version         1.67_py3
set     prefix          /app1/centos6.3/gnu
set     tool            boost

proc ModulesHelp { } {
        global version prefix tool

        puts stderr "\t Adss $tool v$version to environment\n"
}

if { ![is-loaded gcc-7.3.0 ] } {
        module load gcc-7.3.0
}

if { ![is-loaded python3.6.4 ] } {
        module load python3.6.4
}

prereq python3.6.4
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

