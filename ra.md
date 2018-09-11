# Installing Ra 

This is one of the dependency for Jelly2


## Download and build

```
cd /app1/bioinfo/source/git
git clone --recursive https://github.com/rvaser/ra.git ra
cd ra
mkdir build and cd build
module load gcc-4.8.2 cmake
cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/app1/bioinfo/Ra/1.0/ ..

```