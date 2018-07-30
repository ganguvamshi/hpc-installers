# PBSuite

PBJelly is a highly automated pipeline that aligns long sequencing reads (such as PacBio RS reads or long 454 reads in fasta format) to high-confidence draft assembles. PBJelly fills or reduces as many captured gaps as possible to produce upgraded draft genomes. Each step in PBJelly’s workflow can be run on a cluster, thus parallelizing the gap filling process for rapid turn around, even for very large eukaryotic genomes.

https://sourceforge.net/projects/pb-jelly/

## Prerequisites

* Blasr (https://github.com/PacificBiosciences/blasr)
    * Ninja command
    * meson compiler (installed as python package in python3.5)
        * pip3 install meson

* Python 2.7
* Networkx v1.1

## Download 

```
mkdir -p /app1/bioinfo/pbsuite/
cd /app1/bioinfo/pbsuite 
wget -O PBSuite_15.8.24.tgz https://sourceforge.net/projects/pb-jelly/files/PBSuite_15.8.24.tgz/download
tar -xvf PBSuite_15.8.24.tgz
mv PBSuite_15.8.24 15.8.24

```


