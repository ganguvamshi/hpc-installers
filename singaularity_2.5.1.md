## Installing Singulariry v2.5.1

#### Dependencies

tools needed
* squash-tools
* libarchive

### Downloding source 

```
VERSION=2.5.1
wget https://github.com/singularityware/singularity/releases/download/$VERSION/singularity-$VERSION.tar.gz
tar xvf singularity-$VERSION.tar.gz
cd singularity-$VERSION
```

### Build and Install
```
module load squashtools/4.3 libarchive/2.7.0
./configure --prefix=/app1/centos6.3/gnu/singularity/2.5.1
make -j5
make -j5 install

```