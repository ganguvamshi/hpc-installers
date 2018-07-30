# Metassembler

More info can be found here: https://sourceforge.net/projects/metassembler/

## Downlaod 

```
cd /app1/bioinfo
mkdir Metassembler && cd Metassembler
wget -O Metassembler.1.5.tar.gz https://sourceforge.net/projects/metassembler/files/v1.5/Metassembler.1.5.tar.gz/download
tar xvf Metassembler.1.5.tar.gz
mv Metassembler 1.5 && cd 1.5

```

## Compiling and Installation

Metassembler is dependent on Mummer3, Samtools, bowtie2, perl, python

```
module load Mummer3/3.23 samtools/1.6 bowtie2  python2.7 perl5
make check
make install


```
