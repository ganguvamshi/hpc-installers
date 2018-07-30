# BLASR

* prerequisite for PBSuite

**BLASR** can only be built using *Meson*, which uses *Ninja* as command invoking tool.

Ninjs is avaible as a binary in common bin PATH
Meson is installed using python3.5 using pip3

`pip3 install meson`


## Download, Compile and Install

```
git clone git://github.com/PacificBiosciences/blasr.git

LDFLAGS="-L${PATH_TO_HDF5_ROOT}/lib -lhdf5_cpp -lhdf5" \
CPPFLAGS="-isystem ${PATH_TO_HDF5_ROOT}/include" \
meson -Dtests=false build .
ninja -C build
ninja -C build install

```

## STATUS

Cannot install as the menson build gets failed over multiple tries with different options. 
